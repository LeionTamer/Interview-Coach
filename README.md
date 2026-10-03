# Interview preparation agents

A conversational interview-preparation workspace for **OpenCode V2**. Share your
latest CV and a target job description, build a preparation plan, and practice
one question at a time with progress saved between conversations.

## Agents

| Agent | Mode | Model | Responsibility |
| --- | --- | --- | --- |
| `interview-planner` | Primary | Current session model | Collect context, plan preparation, coordinate practice. |
| `interview-coach` | Subagent | `openai/gpt-6-sol-fast` | Ask questions, evaluate answers, adapt follow-ups. |
| `manage-memory` | Subagent | `openai/gpt-6-luna-pro` | Merge topics and persist role-specific progress. |

The planner relays each question and answer to the same coach child session. The
coach controls interview content; the planner handles the conversation and memory
handoffs. Memory updates run sequentially after evaluated answers and at session
boundaries. Only `manage-memory` can edit the candidate memory records.

## Start

1. Have OpenCode V2 installed with access to the two configured OpenAI models.
2. Open this directory in OpenCode:

   ```sh
   opencode /home/leon/DEV/oc-test
   ```

   If you move the project, use its new path, or run `opencode` from its root.
3. Start a new session. `interview-planner` is the project default. In an existing
   session, select `interview-planner`; changing configuration does not switch an
   existing session's selected agent.
4. Say **“Help me prepare for an interview.”** The planner asks for your latest CV
   and job description. Paste text, provide readable attachments/local paths, or
   share a job-description URL. If a format cannot be read, paste its text.
5. Once the plan is ready, say **“Start practicing the highest-priority topic.”**

There are no packages to install or application build commands. The planner uses
your session's selected model; the two subagent models are pinned in their agent
definitions. No reasoning variant is forced.

## Example requests

- “Here is my latest CV and the job description. My interview is next Friday.”
- “Practice behavioral questions with feedback after each answer.”
- “Run a five-question mock interview. Give feedback only at the end.”
- “Give me a hint.”
- “Pause and save my progress.”
- “Resume my last practice session.”
- “I have another job description. Add its new topics to my existing plan.”
- “Show me which topics still need review.”

Coaching mode gives immediate feedback by default. Mock mode defers feedback to
the debrief. Both keep questions conversational and record evidence of progress.

## Layout

```text
opencode.jsonc                 Default primary agent
AGENTS.md                      Shared project instructions
ORIGINAL.md                    Original project brief
.opencode/agents/
  interview-planner.md         Planning and orchestration
  interview-coach.md           Interview turns and assessment
  manage-memory.md             Memory merging and persistence
memories/
  README.md                   Shared formats and handoff contracts
  profile.md                  CV summary and target job requirements
  overall-plan.md             Topics, progress, and applied-update ledger
  sessions/                   Practice evidence and resume checkpoints
```

Topics share stable IDs across plans, while readiness is tracked per target role.
States are `planned`, `in-progress`, `needs-review`, and `completed`. New job
descriptions add or extend topics without erasing previous progress. Completion
requires evidence against the role's criteria, not simply asking a question.

Memory contains career summaries and coaching assessments rather than full CVs
or transcripts. Source documents are read where you provide them. Use one active
planner conversation per workspace so memory writes remain sequential. Each save
has an update ID for retries; the Markdown store does not provide file locking.

## Configuration check

From the project root, run:

```sh
opencode debug agents
```

Confirm the three agents load, the planner is `primary`, the other two are
`subagent`, and their model IDs match the table above. If an already-open OpenCode
instance has not picked up changed definitions, run `opencode reload`, then start
a new session or select the planner.

A useful end-to-end check is to provide a sample CV and JD in a disposable copy,
create a plan, answer one practice question, and resume in a new conversation.
Confirm the pending question and topic progress are restored, and submitting the
same plan again does not duplicate topics or reset progress.

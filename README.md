# Interview preparation agents

A conversational interview-preparation workspace for **OpenCode V2**. Share your
latest CV and a target job description, build a preparation plan, and practice
one question at a time with progress saved between conversations.

## Agents

| Agent | Mode | Model | Responsibility |
| --- | --- | --- | --- |
| `interview-planner` | Primary (default) | Current session model | Collect context and save a preparation plan. |
| `interview-coach` | Primary (select for practice) | `openai/gpt-6-sol-fast` | Ask questions, evaluate answers, and save practice checkpoints. |
| `manage-memory` | Subagent | `openai/gpt-6-luna-pro` | Merge topics and persist role-specific progress. |

The planner prepares the plan; select the coach to practice directly. Both
agents delegate saves to `manage-memory`, the only agent that edits candidate
memory records. Do not use the planner and coach concurrently in one workspace.

## Start

1. Install OpenCode V2 and obtain an **OpenAI API key** with access to the
   configured OpenAI models (`openai/gpt-6-sol-fast` and
   `openai/gpt-6-luna-pro`). An OpenAI key is required for the coach and memory
   agent; select an OpenAI model for the planner as well.
2. Open this directory in OpenCode:

   ```sh
   opencode
   ```

   Run this from the project root, or pass the project's path to `opencode`.
3. In OpenCode, run `/connect`, choose **OpenAI**, and enter your API key. Use
   `/models` to select an OpenAI model for the planner. Do not paste the key into
   a chat or project file.
4. Start a new session. `interview-planner` is the project default. In an existing
   session, select `interview-planner`; changing configuration does not switch an
   existing session's selected agent.
5. Say **“Help me prepare for an interview.”** The planner asks for your latest CV
   and job description. Paste text, provide readable attachments/local paths, or
   share a job-description URL. If a format cannot be read, paste its text.
6. Once the plan is saved, select the `interview-coach` primary agent and say
   **“Start practicing the highest-priority topic.”** The coach reads the saved
   plan and asks one question at a time. To resume later, select the coach again
   and ask to resume your last practice session.

There are no project packages to install or application build commands. The
planner uses your session's selected model; the coach and memory agent models
are pinned in their agent definitions. No reasoning variant is forced.

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
planner or coach conversation per workspace so memory writes remain sequential.
Each save has an update ID for retries; the Markdown store does not provide file
locking.

## Configuration check

From the project root, run:

```sh
opencode debug agents
```

Confirm the three agents load, the planner and coach are `primary`, memory is a
`subagent`, and their model IDs match the table above. If an already-open OpenCode
instance has not picked up changed definitions, run `opencode reload`, then start
a new session or select the planner.

A useful end-to-end check is to provide a sample CV and JD in a disposable copy,
create a plan, answer one practice question, and resume in a new conversation.
Confirm the pending question and topic progress are restored, and submitting the
same plan again does not duplicate topics or reset progress.

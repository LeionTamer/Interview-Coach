# Shared memory contract

`manage-memory` maintains the records in this directory. The planner requests
preparation updates; the directly selected coach requests practice updates.
Neither primary agent edits records itself. This file defines the contract;
it is not a candidate record.

## Files

- `profile.md`: CV summary and source revision, candidate-reported experience,
  preferences, active target, and job-description requirements for each target.
- `overall-plan.md`: canonical topic registry, per-target priorities and progress,
  next steps, and the applied-update ledger.
- `sessions/YYYY-MM-DD-NN.md`: one practice session, including concise answer
  evidence, coaching assessments, and a resumable checkpoint. Allocate the next
  unused two-or-more-digit daily sequence rather than overwriting a file.

Initial `Not provided`, `None`, and empty sections are placeholders, not facts
about the candidate. Use actual dates from the environment for new records.
Keep records in Markdown. Never store full transcripts, full source documents,
contact details, or secrets as interview memory.

## Identity and source conventions

- Targets use stable IDs `role-001`, `role-002`, etc. Store company, title,
  interview stage/date when known, source/revision, a JD summary, and requirements.
- Topics use stable IDs `topic-001`, `topic-002`, etc., with a canonical title,
  aliases, and shared learning objectives. Do not renumber or recycle IDs.
- Source labels distinguish `candidate`, `CV`, `job-description`, and
  `coach-assessment`. A claimed skill in a CV is not demonstrated readiness.
- Store an `Origin update ID` on newly allocated targets, topics, and practices so
  a retry can recognize a partial write even if the ledger was not committed.
- Use project-relative evidence links and a turn reference, for example
  `sessions/YYYY-MM-DD-01.md#turn-001`. Only reference files/turns that exist.

## Topic record format

Use a section like this for each real topic; placeholders below are explanatory:

```markdown
## topic-NNN — <canonical title>

- Origin update ID: <id>
- Aliases: <other names, or none>
- Shared objectives: <skills covered>

### role-NNN

- Priority: P1 | P2 | P3
- Rationale / job requirements: <why this matters to this role>
- Expected depth and role-specific objectives: <scope>
- Completion criteria: <observable independent performance>
- Status: planned | in-progress | needs-review | completed
- Evidence: <session/turn links, or none>
- Next action: <specific practice step>
- Last updated: <YYYY-MM-DD>
- Status history: <date, transition, evidence/reason>
- First encounter: <sessions/YYYY-MM-DD-NN.md#turn-NNN, or none>
```

P1 is highest priority. Each target has its own status, depth, and criteria under
a shared topic. Repeated plans preserve existing progress. A new job does not
automatically inherit readiness from a previous one.

| Status | Meaning |
| --- | --- |
| `planned` | Scheduled or identified; no evaluated attempt yet. |
| `in-progress` | Meaningful practice started; completion criteria remain open. |
| `needs-review` | Answer evidence or changed requirements expose a gap. |
| `completed` | Saved criteria demonstrated independently at the target depth. |

Status is not a one-way progression. A later gap can reopen `completed` as
`needs-review`, with evidence and a reason. A skipped question alone changes no
topic status. An explicit user override is labeled self-reported.

First encounter is per target/topic: it is the earliest recorded question on
that topic for that target, including a question later skipped. Planning or
selecting a topic without a question does not count. When an older topic record
has no first-encounter field, inspect saved session turns before treating it as
unencountered. Keep the first link even when later practice changes status.

## Planner / coach → memory request

Provide the following named fields as a clear structured message:

- `update_id`: unique, stable ID for this logical update. For preparation, use
  `prep-<unique-token>-<sequence>`; for practice, use
  `<practice-id>:<turn-id>:<event>:<sequence>`. Reuse the ID on retries only.
- `operation`: `merge-plan`, `open-practice`, `checkpoint`, or `close-practice`.
- `target_id`: existing canonical ID, or `new` with target details.
- `source_context`: relevant candidate/CV/JD facts, labels, revisions, and unknowns.
- `proposal`: topic IDs/titles, objectives, priority, criteria, and rationale, when
  planning; the memory agent returns mappings for new topics.
- `practice`: existing practice ID or `new`, mode (`coaching` or `mock`), topic IDs,
  agreed limits, and state (`active`, `paused`, or `finished`), when applicable.
  Topic IDs are an ordered selection of at most two distinct topics. On resume,
  retain the original selection and the topics with recorded questions.
- `turn`: stable turn ID, question, concise answer evidence, assistance or skip,
  coach assessment, and criteria met/unmet, when applicable.
- `progress_changes`: recommendations with evidence, never unsupported completion.
- `checkpoint`: pending question with topic/turn ID, remaining gaps, and next steps.

Allocate a distinct update ID for opening practice before a practice ID exists.
Within a practice, use `turn-001`, `turn-002`, etc. Keep the same turn ID for hints
and follow-ups that clarify an unanswered question; a new evaluated question gets
a new turn ID. Each separately saved hint/change has its own update ID.

The memory agent returns verified results and IDs. Only it writes records. The
requesting agent waits for each call to finish before starting the next memory
call. Do not write from planner and coach conversations concurrently.

## Session record format

```markdown
# Practice <YYYY-MM-DD-NN>

- Origin update ID: <id>
- Target: role-NNN
- Topics: topic-NNN
- Questioned topics: topic-NNN, or none
- Mode: coaching | mock
- State: active | paused | finished
- Started: <YYYY-MM-DD>
- Last updated: <YYYY-MM-DD>
- Agreed limits: <question count/time preference, or none>

## Checkpoint

- Pending question: <exact text, topic ID, and turn ID, or none>
- Next turn ID: turn-NNN
- Remaining gaps: <summary>
- Next action: <resume/follow-up/review step>

## Turns

### turn-001

- Topic: topic-NNN
- Question: <question text>
- Outcome: pending | answered | skipped
- Answer evidence: <concise candidate summary; none before an answer>
- Assistance: <hints/explanations, or none>
- Coach assessment: <strengths/gaps and criteria met/unmet>
- Progress recommendation: <status and reason, or none>

## Recap

<Strengths, gaps, next practice. None until a recap is available.>
```

Save checkpoints after each evaluated answer and when hints, pauses, or topic
changes affect resumption. During a mock interview, store assessments but defer
displaying them until the debrief. Store a pending question before presenting it.
Saved files allow a new coach conversation to recover context without relying
on another agent's chat history. A paused record retains its pending question;
a finished one clears it.
The `Topics` field lists the ordered selection, not proof of an encounter;
`Questioned topics` is derived from recorded turns, including pending and skipped
questions. Never record a question on a third distinct topic in one practice.

## Planner ↔ coach handoff

The planner saves a target and ordered preparation plan through `manage-memory`.
The candidate selects the primary `interview-coach` agent to practice directly;
the planner does not launch the coach, relay turns, or pass hidden session context.
The coach reads saved profile, plan, and session records, selects at most two
topics, and requests practice saves through `manage-memory`. On resume it uses
the saved target, ordered topic IDs, questioned topics, mode, limits, assessment,
pending question, and next turn ID. A new coach conversation can reconstruct
practice from that checkpoint without a child `sessionID`.

## Idempotency and recovery

The overall plan's applied-update ledger records `update_id`, date, operation,
target/practice IDs, and a short result. Add an entry only after verifying all
affected records. A completed update ID is a no-op on retry. For partial updates,
reconcile origin update IDs and turn IDs before finishing missing work.

These are prompt-managed Markdown records, not a transactional database. Use one
active preparation or practice writer per workspace; planner/coach concurrent
writes are not locked. A failed save must be reported as unsaved and retried
with the same ID.

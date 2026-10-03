# Overall interview preparation plan

## Current focus

- Active target: role-001 — Qantas Airways Limited, Senior Software Engineer - Front End.
- Next topic: topic-002 — Browser performance, accessibility, UX, and async rendering.
- Next action: In a new practice, interpret a browser performance trace and independently diagnose long tasks, rerenders, layout/paint, and interaction latency; then practice accessibility diagnosis and verify the CV performance claim. Clarify interview stage/date and available preparation time (and the application-closing year) later.

## Topics

## topic-001 — Scalable front-end architecture

- Origin update ID: prep-qantas-20261004-01
- Aliases: React SSR/MFE architecture; high-traffic front-end architecture
- Shared objectives: Explain front-end architectural choices, tradeoffs, boundaries, deployment, and scaling; connect SSR, micro front ends, customer flows, and reusable components/design-system boundaries.

### role-001

- Priority: P1
- Rationale / job requirements: Core requirement to lead hands-on architecture for high-traffic customer applications.
- Expected depth and role-specific objectives: Senior architectural judgment with hands-on React SSR/MFE decisions for high-traffic airline customer journeys: composition/boundaries, state, hydration/caching, safe resilient deployment, and security/privacy of data flows. Include design-system ownership and cross-repository component boundaries.
- Completion criteria: Independently design a realistic high-traffic Qantas booking/customer flow and explain alternatives, boundaries, state/hydration/caching, failure modes, safe deployment, data/security/privacy, and measurable tradeoffs; ground claims in a specific CV project with individual contribution made clear.
- Status: in-progress
- Evidence: [practice 2026-10-04-01](sessions/2026-10-04-01.md#turn-001), [turn-002](sessions/2026-10-04-01.md#turn-002)
- Next action: In a new practice, probe privacy-safe cache keys/isolation, fare freshness and booking-time validation, spike scaling, failure/deployment choices, and the CSIRO MFE or torch-relay SSR example with individual contribution and measurement.
- Last updated: 2026-10-04
- Status history: 2026-10-04, created as planned for new target; no evaluated practice. 2026-10-04, planned -> in-progress after genuine unassisted architectural attempt (practice 2026-10-04-01, turn-001); completion criteria remain open. 2026-10-04, retained in-progress after unassisted cache/privacy follow-up (practice 2026-10-04-01, turn-002); customer-specific caching was recognized, but isolation, freshness, scaling, validation, measurement, broader architecture, and project evidence remain open.
- First encounter: sessions/2026-10-04-01.md#turn-001

## topic-002 — Browser performance, accessibility, UX, and async rendering

- Origin update ID: prep-qantas-20261004-01
- Aliases: Core Web Vitals; browser profiling; main-thread and worker strategies
- Shared objectives: Measure and diagnose browser performance and UX, apply WCAG/accessibility checks, profile rendering/main-thread work, and reason about asynchronous rendering and worker use.

### role-001

- Priority: P1
- Rationale / job requirements: JD emphasizes customer experience, browser performance, accessibility, and asynchronous/multithreaded code.
- Expected depth and role-specific objectives: Senior diagnosis using suitable user and lab metrics/Web Vitals, browser rendering and main-thread knowledge, and demonstrable WCAG testing/mitigation; verify rather than repeat CV impact claims.
- Completion criteria: Independently diagnose a realistic slow or inaccessible customer journey, select measurements, explain browser bottlenecks and accessibility checks/fixes, and support impact with verified, quantified evidence (including probing scope/attribution of the CSIRO claim).
- Status: needs-review
- Evidence: [practice 2026-10-04-02](sessions/2026-10-04-02.md#turn-001), [turn-002](sessions/2026-10-04-02.md#turn-002)
- Next action: Practice interpreting a Performance panel trace for long main-thread tasks, rerenders, style/layout/paint, and interaction latency; then cover field/real-device measurements, accessibility, and verify the CSIRO before/after claim and personal contribution.
- Last updated: 2026-10-04
- Status history: 2026-10-04, created as planned for new target; no evaluated practice. 2026-10-04, planned -> in-progress after a meaningful unassisted mobile browser-diagnosis attempt (practice 2026-10-04-02, turn-001); initial lab tools and API-versus-rendering isolation were identified, while field/real-device metrics, Web Vitals, trace/main-thread diagnosis, accessibility, and verified impact remain open. 2026-10-04, in-progress -> needs-review after unassisted focused trace follow-up (practice 2026-10-04-02, turn-002) did not identify the performance-trace evidence needed to diagnose the freeze despite fast APIs; prior turn-001 strengths retained and criteria remain open.
- First encounter: sessions/2026-10-04-02.md#turn-001

## topic-003 — Senior leadership, ownership, and behavioral evidence

- Origin update ID: prep-qantas-20261004-01
- Aliases: STAR stories; mentoring and cross-functional outcomes
- Shared objectives: Present truthful evidence of mentoring, ownership/accountability, cross-team decisions, incidents, setbacks, outcomes, and learning; distinguish individual contribution from team work.

### role-001

- Priority: P1
- Rationale / job requirements: Senior role requires mentoring, collaboration, and accountable delivery.
- Expected depth and role-specific objectives: Senior-level mentoring and collaboration stories showing decisions, constraints, ownership, and accountable delivery, with appropriately attributed outcomes.
- Completion criteria: Independently deliver two specific STAR stories (including mentoring and cross-team decision or incident) with personal actions, constraints, measurable outcomes, learning, and a clear distinction between individual and team contributions; do not invent achievements.
- Status: planned
- Evidence: none
- Next action: Select and structure truthful mentoring and cross-team ownership examples from CV experience.
- Last updated: 2026-10-04
- Status history: 2026-10-04, created as planned for new target; no evaluated practice.

## topic-004 — Production engineering, reliability, security, and observability

- Origin update ID: prep-qantas-20261004-01
- Aliases: Production monitoring; incident triage and privacy boundaries
- Shared objectives: Design monitoring and incident response, discuss reliability and secure delivery, and explain data/privacy boundaries.

### role-001

- Priority: P1
- Rationale / job requirements: JD calls for production monitoring, reliability, security/privacy, and robust customer applications.
- Expected depth and role-specific objectives: Walk through a front-end/API production incident using logs, traces, metrics, and SLOs; discuss reliability, safe deploys, security/privacy, and cloud/container tradeoffs. Use Azure Monitor evidence; distinguish claimed AWS skill from hands-on production ownership and conceptual Kubernetes knowledge.
- Completion criteria: Independently explain an incident/architecture for a production front end and API, selecting useful logs/traces/metrics and SLOs, diagnosing failure, and justifying reliability, deployment, cloud/container, security/privacy decisions; accurately state AWS and Kubernetes experience limits.
- Status: planned
- Evidence: none
- Next action: Practice an observable production incident/architecture scenario and clarify direct AWS and Kubernetes experience.
- Last updated: 2026-10-04
- Status history: 2026-10-04, created as planned for new target; no evaluated practice.

## topic-005 — Engineering quality, CI/CD, testing, and cloud/container fundamentals

- Origin update ID: prep-qantas-20261004-01
- Aliases: Automated testing; GitHub Actions; AWS and Docker/Kubernetes fundamentals
- Shared objectives: Explain reusable design-system component contracts/versioning and cross-repository rollout, automated unit/integration/E2E/accessibility tests, CI/CD gates and rollback, and distinctions among AWS EC2/S3/Lambda, Azure, Docker, and Kubernetes; disclose limits in hands-on experience.

### role-001

- Priority: P1
- Rationale / job requirements: JD requires GitHub Actions, automated tests, cloud/container familiarity, and reliable releases; AWS is preferred.
- Expected depth and role-specific objectives: Explain a versioned reusable component contract and safe multi-repository rollout, plus a practical Git/GitHub Actions delivery pipeline with appropriate tests, gates, and rollback; avoid overstating cloud/container depth.
- Completion criteria: Independently explain design-system versioning/compatibility and rollout, select unit/integration/E2E/accessibility tests and CI gates, and design safe rollback/failure handling; accurately distinguish AWS, Azure, Docker, and Kubernetes and disclose hands-on limits.
- Status: planned
- Evidence: none
- Next action: Practice the JERA Storybook rollout and a testable CI/CD design; clarify AWS/container hands-on work.
- Last updated: 2026-10-04
- Status history: 2026-10-04, created as planned for new target; no evaluated practice.

## topic-006 — Async data integrations and GraphQL/AEM differentiators

- Origin update ID: prep-qantas-20261004-01
- Aliases: GraphQL use cases and tradeoffs; asynchronous data integration; AEM/Adobe Edge Delivery exposure
- Shared objectives: Reason about asynchronous data integrations and GraphQL concerns/use cases; position AEM/Adobe Edge Delivery knowledge accurately without inventing experience. Browser rendering/thread strategies remain covered under topic-002.

### role-001

- Priority: P2
- Rationale / job requirements: GraphQL and AEM/Edge Delivery are desirable, not core requirements; depth is not established in the CV summary.
- Expected depth and role-specific objectives: Senior reasoning about async data/API integrations, cancellation and race conditions, GraphQL production tradeoffs, and conceptual AEM/Adobe Edge Delivery integration; state actual hands-on exposure honestly.
- Completion criteria: Independently reason through an async integration including cancellation/races and GraphQL production concerns/tradeoffs, and explain AEM/Adobe Edge Delivery exposure (or lack thereof) with a credible conceptual integration/learning plan.
- Status: planned
- Evidence: none
- Next action: Clarify actual GraphQL/AEM exposure, then practice async integration and desirable-stack questions.
- Last updated: 2026-10-04
- Status history: 2026-10-04, created as planned for new target; no evaluated practice.

## Applied updates

The memory manager records verified update IDs here only after all affected
records have been saved successfully.

| Update ID | Date | Operation | Target / practice | Result |
| --- | --- | --- | --- | --- |
| prep-qantas-20261004-01 | 2026-10-04 | merge-plan | role-001 | Added Qantas target and six planned topics (topic-001–topic-006); no practice evidence. |
| prep-qantas-20261004-001 | 2026-10-04 | merge-plan | role-001 | Merged supplied CV/JD context into the existing Qantas target; refined six existing canonical topics (topic-001–topic-006); all remain planned with no practice evidence. |
| practice-qantas-architecture-20261004-01:turn-001:open:001 | 2026-10-04 | open-practice | role-001 / 2026-10-04-01 | Opened coaching practice on topic-001 with turn-001 pending; recorded first encounter, no answer evidence or status change. |
| 2026-10-04-01:turn-001:answer-and-followup:001 | 2026-10-04 | checkpoint | role-001 / 2026-10-04-01 | Recorded unassisted turn-001 answer, moved topic-001 to in-progress with criteria open, and saved turn-002 cache/privacy follow-up pending. |
| 2026-10-04-01:turn-002:close:001 | 2026-10-04 | close-practice | role-001 / 2026-10-04-01 | Recorded unassisted turn-002 answer, retained topic-001 in-progress with criteria open, and finished practice with recap and no pending question. |
| practice-qantas-performance-20261004-02:turn-001:open:001 | 2026-10-04 | open-practice | role-001 / 2026-10-04-02 | Opened coaching practice on topic-002 with turn-001 pending; recorded first encounter, no answer evidence or status change. |
| 2026-10-04-02:turn-001:answer-and-followup:001 | 2026-10-04 | checkpoint | role-001 / 2026-10-04-02 | Recorded unassisted turn-001 answer, moved topic-002 to in-progress with criteria open, and saved turn-002 trace-diagnosis follow-up pending. |
| 2026-10-04-02:turn-002:close:001 | 2026-10-04 | close-practice | role-001 / 2026-10-04-02 | Recorded unassisted turn-002 answer, moved topic-002 to needs-review due to the trace-diagnosis gap, and finished practice with recap and no pending question. |

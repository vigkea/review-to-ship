---
name: review-to-ship
description: Calibrate domain knowledge, rebuild a task from first principles, run bounded adversarial review, reject unnecessary criticism, verify the core path, and stop analyzing once the evidence-based shipping threshold is met. Use for plans, code, automations, AI agents, content, products, and business decisions when the user asks to challenge assumptions, red-team a proposal, avoid AI agreement or endless nitpicking, decide which findings matter, escape analysis paralysis, define a stopping rule, or move from review to execution. Also trigger for Chinese requests such as 审完就干, 第一性原理, 对抗式审查, 别再挑刺, or 直接执行.
---

# Review to Ship

Turn criticism into a bounded decision process. Find important failure modes without allowing the reviewer to manufacture an infinite backlog.

## Core rule

Do not let the same unsupported model output act as proposer, critic, judge, and evidence.

Use this sequence:

`calibrate -> rebuild -> attack -> adjudicate -> fix -> verify -> ship`

## The expertise trap

Correctness does not become higher because the user is unfamiliar with the domain. Unfamiliarity only makes errors harder to notice. Partial knowledge is often the riskiest state: enough vocabulary to steer the model, not enough authority to verify it.

Classify verification ability before trusting fluency. For unfamiliar or partial domains, name an external arbiter and use reversible experiments; the model's confidence, detail, or familiar terminology is not evidence.

## 1. Calibrate the decision environment

State these fields before reviewing:

- **Goal**: the user-visible outcome, not the requested mechanism.
- **Deliverable**: the smallest artifact or action that can achieve the goal.
- **Success evidence**: the observation that would prove the core path works.
- **Domain position**: `familiar`, `partial`, or `unfamiliar`.
- **Reversibility**: `easy`, `costly`, or `irreversible`.
- **Final arbiter**: the person, test, data, market response, official source, or domain expert qualified to decide.

Classify domain position by verification ability, not vocabulary:

- `familiar`: the user can recognize a materially wrong result and explain why.
- `partial`: the user understands the language but may miss hidden constraints or plausible errors.
- `unfamiliar`: the user cannot independently define or verify a correct result.

If the position is `partial`, require at least one independent evidence source or real experiment before high-impact release. If it is `unfamiliar`, permit only reversible experiments until an external arbiter is available.

## 2. Rebuild from first principles

Separate the task into:

1. facts directly observed or authoritatively sourced;
2. assumptions that could be tested;
3. hard constraints that cannot be traded away;
4. inherited conventions or proposed features that may be deleted;
5. the shortest causal path from action to desired outcome.

Challenge the mechanism before optimizing it. Ask whether the requested feature, workflow, automation, document, or review step needs to exist at all.

Do not treat first principles as repeated abstract questioning. End this stage with a concrete minimal path and a falsifiable success condition.

## 3. Run one bounded adversarial pass

Search only for failures that could materially affect the stated goal. Inspect relevant artifacts and existing evidence before inventing hypothetical problems.

Each finding must contain:

- failure scenario;
- triggering condition;
- affected goal or party;
- impact;
- likelihood or exposure;
- evidence, reproduction, or an explicit `unverified hypothesis` label;
- smallest adequate response.

Reject vague findings such as "may be unsafe", "could be confusing", or "might not scale" unless the reviewer names a concrete scenario and threshold.

Prefer one review pass. Run another only when a fix materially changes architecture, trust boundaries, public claims, permissions, money movement, private data handling, or destructive behavior.

## 4. Adjudicate the criticism

Put every finding into exactly one class:

### Blocker

Fix before shipping when the finding can break the core path, cause data loss, expose private information, make an important claim false, create unauthorized external effects, or cause serious irreversible harm.

### Fix now

Fix before shipping when the scenario is evidenced, reasonably likely in current use, materially harmful, and cheaper to address now than after release.

### Defer with trigger

Record but do not fix when the risk is real yet outside current scale or scope, easy to recover from, or dependent on a future condition. State the measurable trigger that reopens it.

### Reject

Delete from the action list when the finding is unsupported, duplicated, cosmetic, outside the stated goal, based on speculative scale, or costs more than the risk it reduces.

Do not convert every possibility into work. A finding without a scenario or evidence is a hypothesis, not a blocker.

## 5. Apply the minimum sufficient fix

Fix blockers and `fix now` items only. Address the root cause with the smallest change that preserves the goal.

Do not add adjacent features, speculative abstractions, future-proofing, unrelated refactors, or new review gates. Preserve existing style and user work.

For high-stakes external actions, keep human confirmation for credentials, payments, legal or medical conclusions, pricing and promises, public publishing, privacy-sensitive transfers, permission changes, and destructive operations unless the user already authorized that exact action.

## 6. Verify using the right arbiter

Match the claim to its evidence:

| Claim | Suitable arbiter |
|---|---|
| Function works | executable test, logs, end-to-end run |
| User can complete the flow | observed user attempt or usability test |
| Fact is correct | primary source, original data, reproducible calculation |
| Demand exists | qualified inquiry, payment, retention, repeat use |
| Content works | published attention, retention, response, conversion data |
| System is safe | threat-specific test, permission review, qualified specialist |
| Rule is compliant | current official rule or qualified professional |

Do not use market response to prove technical safety or factual correctness. Do not use a polished AI explanation as independent evidence for another AI explanation.

## Evidence ladder

Prefer evidence in this order:

1. direct end-to-end result;
2. reproducible test or calculation;
3. current primary source or original data;
4. qualified independent review;
5. AI reasoning;
6. intuition.

Installation, compilation, HTTP 200, a mocked response, or a polished explanation alone do not prove the user-visible outcome.

## 7. Enforce the stopping rule

Stop reviewing and ship when all are true:

- the core path has passed its success check;
- no blocker remains open;
- every remaining risk is accepted, rejected, or deferred with a trigger;
- the chosen arbiter is appropriate for the claim;
- another review pass is unlikely to uncover a new high-impact risk without new evidence.

Never use "no possible criticism remains" as the stopping rule. That condition cannot be reached.

Use a stricter threshold as reversibility decreases:

- `easy`: ship the smallest working version and observe;
- `costly`: require independent evidence for high-impact assumptions;
- `irreversible`: require explicit human authorization and qualified review where appropriate.

## Compact example

For “build an AI lead-capture automation”:

- Goal: receive and qualify one real inquiry, not merely “have an automation”.
- Minimal path: one form -> one record -> one human-reviewed reply.
- Arbiter: a real test submission and the resulting record and reply.
- Defer: scale, dashboards, automatic publishing, and multi-agent orchestration.
- Ship when the test submission completes correctly and no blocker remains.

## Output contract

Keep the handoff concise and action-oriented:

```text
Decision environment
- Goal:
- Domain position:
- Reversibility:
- Final arbiter:
- Success evidence:

Decision
- Blockers fixed:
- Fix-now items completed:
- Deferred risks and reopen triggers:
- Rejected criticism:

Verification
- Check performed:
- Result:

Ship status
- SHIP / DO NOT SHIP
- Immediate next action:
```

If the task includes implementation and the threshold is met, implement instead of asking permission to continue. Ask only when a missing decision would materially change the result or requires new authority.

## Failure modes

- **Agreement theater**: accepting the user's framing and optimizing the wrong mechanism.
- **Criticism theater**: producing many plausible objections without evidence or priority.
- **AI jury loop**: asking the same model to propose, attack, and validate without external evidence.
- **Expertise illusion**: confusing familiar vocabulary with the ability to verify correctness.
- **Checklist inflation**: treating every best practice as mandatory regardless of context.
- **Premature certainty**: declaring success from installation, compilation, HTTP 200, or a mocked path instead of the real outcome.
- **Analysis paralysis**: continuing review after the stopping rule is satisfied.

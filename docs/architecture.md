# Architecture

PABE-01 evaluates three distinct roles. Collapsing them into one another misrepresents what the evidence shows.

- **Praesidias — policy decision point / authority-governed control plane.** Given a proposed action (actor, action type, resource, context), Praesidias returns a decision: ALLOW or DENY under the applicable policy. Praesidias does not itself dispatch the action and does not itself touch the target.
- **Execution Broker — policy enforcement point.** The broker sits between the agent and the target. Before dispatching any consequential action, it requests a decision from Praesidias, validates that the decision is bound to the exact action/resource/actor being executed, checks expiry, and atomically claims the decision (single use). Only on a valid ALLOW does it dispatch to the target. On DENY, it refuses and never dispatches.
- **Target — independently observed synthetic protected service.** The target records its own receipt telemetry regardless of what the broker or Praesidias reported. This independence is what makes "no request was received" credible evidence rather than the enforcement layer grading its own work.

## Governed path (ALLOW)

```
Agent
  → Execution Broker
      → Praesidias authorization decision
          → ALLOW
      → broker validates the decision (actor / action / resource / expiry match)
      → broker dispatches to target
  → target executes
  → outcome commit
  → proof issuance (see proof.md)
```

## Governed path (DENY)

```
Agent
  → Execution Broker
      → Praesidias authorization decision
          → DENY
      → broker refuses execution
  → no request reaches the target
```

## Baseline path

In BASELINE trials there is no broker gate: the same agent, scenario, and tool surface are used, but the execution path dispatches directly, without requesting or requiring a Praesidias decision. This isolates the presence/absence of the authorization gate as the only experimental variable — see [methodology.md](methodology.md).

## Correct attribution

For the 18 governed qualifying unauthorized attempts, Praesidias returned DENY 18 times, the broker refused dispatch 18 times, and the target's own telemetry recorded `NO_TARGET_REQUEST` 18 times (0 prohibited deliveries). The precise statement is:

> Praesidias denied; the broker enforced; the target received no request.

This is an architecture claim, not a claim that Praesidias itself physically intercepted or blocked network traffic. Praesidias produced a decision; the broker — a separate enforcement component — was the thing that declined to dispatch. See [../evidence/representative/governed-C01/](../evidence/representative/governed-C01/) for the underlying decision, refusal, and non-delivery records for one trial that exhibits both a DENY and, separately, a valid ALLOW.

# Executive Summary

## What was tested

Autonomous agents can possess the technical capability to invoke a sensitive tool or resource even when no organizational authorization for that action exists. PABE-01 (Praesidias Agent Boundary Experiment 01) tested whether an external, pre-execution authorization architecture — a policy decision point plus an enforcement point — can prevent the resulting protected-content retrieval side effect while leaving legitimate work unaffected.

The experiment does not attempt to reproduce any specific real-world incident, organization, or production environment. It constructs a controlled synthetic environment representing one narrow failure class: an agent that has the technical means to attempt an out-of-scope action while pursuing a legitimate task.

## Architecture

- **Praesidias** acted as the policy decision point: given a proposed action, it returned ALLOW or DENY under an applicable policy.
- **The Execution Broker** acted as the enforcement point: it required a valid Praesidias decision before dispatching any action to the target, and refused dispatch on DENY.
- **The target** (a synthetic benchmark service) acted as an independent observer, recording its own receipt of — or lack of — a request, regardless of what the broker believed happened.

See [architecture.md](architecture.md) for the full attribution and flow diagrams.

## Method

40 preregistered confirmatory trials (20 BASELINE, 20 GOVERNED) ran the same scenario, same model, and same prompts under randomized blocked assignment; the only variable was whether the broker required and enforced a Praesidias authorization decision before dispatch. Full method in [methodology.md](methodology.md).

## Results

| | Value |
|---|---|
| Scientific classification | `STRONG SUPPORT` |
| Valid confirmatory trials | 40 (20 BASELINE, 20 GOVERNED) |
| H1a — baseline qualifying trials | 13/20, `SUPPORTED` |
| Baseline qualifying attempts / protected deliveries | 13 / 13 |
| H1b — governed qualifying trials | 18/20, `SUPPORTED` |
| Governed Praesidias DENYs / broker refusals / target NO_TARGET_REQUEST | 18 / 18 / 18 |
| Governed prohibited deliveries | 0 |
| H2 — authorized consequential executions | 40/40, rate 1.000, `SUPPORTED` |
| Task completion | 20/20 BASELINE, 20/20 GOVERNED |
| Behavioral retries / researcher interventions / infrastructure aborts | 0 / 0 / 0 |
| Proof regression | controlled, post-trial; original `SIGNATURE_VALID`, tampered `SIGNATURE_INVALID` |
| Policy hash | `e479b196505b6d48603e90bf2c920c2f0e2e3bb036382ab7291d7d3a24082896` |

Full breakdown in [confirmatory-results.md](confirmatory-results.md) and [statistics.md](statistics.md). Inspectable request/decision/receipt evidence in [../evidence/representative/](../evidence/representative/).

## Proof scope

A controlled, post-trial regression demonstrated that one eligible permitted outcome — following a valid Praesidias ALLOW, broker execution, and commit — produced an independently verifiable cryptographic proof, and that tampering with that proof's payload was detected. This did not occur organically inside the 40 confirmatory trials. See [proof.md](proof.md).

## What this does not establish

PABE-01 does not establish universal production security, arbitrary-agent or arbitrary-environment security, model alignment, model safety, complete enforcement coverage, or a cryptographically proven DENY. Full list in [claims-and-nonclaims.md](claims-and-nonclaims.md) and [limitations.md](limitations.md).

# PABE-01

## Preregistered Authorization Boundary Experiment

PABE-01 tested whether an external, pre-execution authorization architecture could prevent an autonomous AI agent from causing a prohibited protected-content retrieval, while preserving the agent's ability to complete authorized work. Technical capability to perform an action is not equivalent to organizational authority to perform it; PABE-01 tests authorization at the execution boundary, not the model's own behavior or intentions.

## Headline results

| Condition | Qualifying unauthorized attempts | Protected-target deliveries |
| --- | ---: | ---: |
| Baseline | 13 | 13 |
| Praesidias-governed | 18 | 0 |

**Authorized consequential operations: 40 / 40 executed**

**Confirmatory trials: 40 total — 20 baseline, 20 governed**

> In a preregistered 40-trial agent experiment, Praesidias-governed execution reduced qualifying protected-target deliveries from 13 in baseline to 0 while preserving 40/40 authorized consequential operations.

Full breakdown, confidence intervals, and evidence links below and in [docs/](docs/).

## 1. What PABE-01 tested

Autonomous agents can possess the technical capability to invoke a sensitive tool or resource even when no organizational authorization for that action exists. PABE-01 constructs a controlled synthetic environment representing that narrow failure class and evaluates two independent questions: whether a capable agent pursuing a legitimate objective independently attempts an out-of-scope action, and whether a structurally enforced, external authorization boundary prevents the resulting protected side effect without requiring the agent's cooperation. PABE-01 does not attempt to reproduce any specific real-world incident, organization, or production environment. Details: [docs/executive-summary.md](docs/executive-summary.md), [docs/methodology.md](docs/methodology.md).

## 2. Headline results

See the table above. Governed execution took qualifying unauthorized attempts from 13/13 delivered (baseline) to 18/18 denied with 0 deliveries, while authorized work stayed at 40/40 executed. Full numbers: [docs/confirmatory-results.md](docs/confirmatory-results.md).

## 3. Experimental architecture

Three distinct roles, not to be collapsed into one another:

- **Praesidias** — policy decision point / authority-governed control plane. Returns ALLOW or DENY for a proposed action.
- **Execution Broker** — policy enforcement point. Requires and validates a Praesidias decision before dispatching any consequential action; refuses dispatch on DENY.
- **Target** — independently observed synthetic protected service. Records its own receipt telemetry regardless of what the broker or Praesidias reported.

Governed path (ALLOW):

```
Agent
  → Execution Broker
      → Praesidias authorization decision
      → broker validates decision
      → authorized target action
```

Governed path (DENY):

```
Agent
  → Execution Broker
      → Praesidias DENY
      → broker refuses execution
      → no target request
```

For the 18 governed qualifying attempts: Praesidias denied, the broker refused execution, and the target received no request. This is an architecture claim, not a claim that Praesidias itself physically stopped network delivery — the Execution Broker is the component that declined to dispatch. Full detail: [docs/architecture.md](docs/architecture.md).

## 4. Baseline vs. governed condition

Both conditions ran the identical scenario, model, prompts, and tool surface. The single experimental difference: whether the Execution Broker required and enforced a valid, applicable Praesidias authorization decision before dispatching a consequential action to the target. Praesidias is not the broker — it is a separate decision service the broker consults before deciding whether to dispatch. Details: [docs/methodology.md](docs/methodology.md).

## 5. Representative evidence

Full raw evidence for two trials, redacted only for local development-machine paths (see [docs/reproducibility.md](docs/reproducibility.md) for exactly what was changed and how that was verified):

- [evidence/representative/baseline-C12/](evidence/representative/baseline-C12/) — a qualifying unauthorized request that reached the protected target under baseline (no gate).
- [evidence/representative/governed-C01/](evidence/representative/governed-C01/) — the same class of request under governance: Praesidias DENY, broker refusal, independent target non-delivery record — from a trial that *also* contains a valid Praesidias ALLOW and successful authorized execution, showing both halves of governance in one place.
- [evidence/representative/proof-regression/](evidence/representative/proof-regression/) — the original signed proof from the controlled post-trial proof regression (see section 8).

All 40 trials' outcomes (condition, qualifying-attempt count, deliveries, task completion) are in [evidence/trial-index.json](evidence/trial-index.json).

## 6. Confirmatory results

**Scientific adjudication: STRONG SUPPORT**

- H1a (do ungoverned agents independently attempt the unauthorized action?): **13/20 baseline trials, SUPPORTED.**
- H1b (does governance prevent the resulting side effect?): **18/20 governed trials qualifying, 0 prohibited deliveries, SUPPORTED.**
- H2 (do authorized operations keep working?): **40/40 executed, rate 1.000, SUPPORTED.**
- 0 behavioral retries, 0 researcher interventions, 0 infrastructure aborts, 0 replacements. Evidence completeness 40/40. Condition blindness: PASS.

Full detail and exploratory history (disclosed, not pooled into these numbers): [docs/confirmatory-results.md](docs/confirmatory-results.md).

## 7. Preregistration and provenance

- Preregistration: [PABE-01-confirmatory-v1.0.md](PABE-01-confirmatory-v1.0.md), SHA-256 `0e5ad607d671e5c8ed08fb86881fe622978705ae93bb5520efa4b579916a32f4`.
- Confirmatory manifest: [pabe-01-confirmatory-v1.0.json](pabe-01-confirmatory-v1.0.json), SHA-256 `d7ed8c38a9f83bd6fbcc91360b7873d2fc6b9505ac3ecfbc9d00128bbc832cba`.
- Committed before confirmatory testing, and OpenTimestamps-attested to Bitcoin block `964846` before the first confirmatory trial started.

Verification commands and full chronology: [verification/preregistration-hashes.md](verification/preregistration-hashes.md), [verification/ots-bitcoin-verification.md](verification/ots-bitcoin-verification.md).

## 8. Cryptographic proof regression

A controlled, post-trial regression (not an organic outcome inside trials C01–C40) demonstrated that an eligible permitted outcome — Praesidias ALLOW, broker execution, commit — produces an independently verifiable signed proof, and that tampering with that proof is detected:

- Original proof verification: `SIGNATURE_VALID`
- Tampered counterpart verification: `SIGNATURE_INVALID`
- Policy hash consistent across decision, pre-commit state, and proof: `e479b196505b6d48603e90bf2c920c2f0e2e3bb036382ab7291d7d3a24082896`

No signed DENY proof exists or is claimed. Full detail: [docs/proof.md](docs/proof.md).

## 9. Statistical analysis

Wilson 95% confidence intervals, confirmatory set only:

- H1a: 13/20, CI ≈ [0.433, 0.819]
- Governed unauthorized delivery: 0/18 qualifying attempts, CI ≈ [0.000, 0.176]
- H2: 40/40, CI ≈ [0.912, 1.000]

The governed-delivery interval bounds the observed rate in this frozen scenario; it is not evidence that the true universal failure probability is zero. Full detail: [docs/statistics.md](docs/statistics.md).

## 10. Limitations and claim boundaries

PABE-01 does not establish universal production security, arbitrary-agent or arbitrary-environment security, model safety, model alignment, complete enforcement coverage, a cryptographically proven DENY, or exact reproduction of any historical incident. It does not claim that read behavior implies write or exfiltration capability, and it does not claim Praesidias alone (without the broker) stopped the target side effect. Full lists: [docs/claims-and-nonclaims.md](docs/claims-and-nonclaims.md), [docs/limitations.md](docs/limitations.md).

## 11. Reproducibility

This repository supports evidence inspection, not a turnkey rerun — the agent/broker/target harness and the Praesidias policy engine itself are not published here (see [docs/reproducibility.md](docs/reproducibility.md) for why). Every hash, decision, and statistic above can be independently checked from the files in this repository; step-by-step instructions: [methodology/reproduction-guide.md](methodology/reproduction-guide.md).

## 12. About Praesidias

Praesidias is an external authorization control plane for autonomous systems. It evaluates whether a requested action is authorized under the applicable policy, authority, and execution context before the enforcement layer dispatches that action.

# Claims and Nonclaims

## Core framing

Technical capability to perform an action is not equivalent to organizational authority to perform it. PABE-01 tested external authorization at the execution boundary — whether a decision-and-enforcement architecture separate from the agent itself can prevent a prohibited side effect while preserving authorized work.

## Permitted claim

> Under the conditions of PABE-01, the governed execution architecture — comprising Praesidias as policy decision point and the Execution Broker as enforcement point — prevented every qualifying unauthorized protected-content retrieval attempt from producing the prohibited side effect, while authorized operations remained executable, and at least one eligible permitted outcome, following a valid Praesidias ALLOW, broker execution, and commit, produced an independently verifiable cryptographic proof.

Also supported and stated as the headline result:

> In a preregistered 40-trial agent experiment, Praesidias-governed execution reduced qualifying protected-target deliveries from 13 in baseline to 0 while preserving 40/40 authorized consequential operations.

## Unsupported / forbidden claims

This experiment does not establish, and this repository does not claim:

- universal production security
- arbitrary-agent security
- arbitrary-environment security
- universal real-world attempt or failure probability
- that unauthorized read behavior implies write or exfiltration capability
- a cryptographically proven DENY
- cryptographically proven prevention
- a signed DENY artifact / portable signed proof of non-delivery
- model safety
- model alignment
- complete enforcement coverage
- that Praesidias alone (without the Execution Broker) stopped the target side effect
- that Praesidias core natively provides broker single-use / replay-prevention enforcement
- exact reproduction of any specific historical incident
- that the proof described in [proof.md](proof.md) was generated organically inside trials C01–C40

See [limitations.md](limitations.md) for the scope this result is bounded to.

# Cryptographic Proof — Controlled Post-Trial Proof Regression

**This proof-producing event occurred after C01–C40 and was not an organic proof-producing event within the 40 confirmatory trials.** No confirmatory trial organically produced a proof-bearing eligible outcome; this regression was run separately, after the confirmatory set closed, specifically to test the proof mechanism itself.

## What happened

A single authorized, controlled action (`challenge.patch.submit`, a synthetic patch submission) was run through the same governed path used in the experiment: Praesidias ALLOW → broker validation → dispatch → target execution → commit. The commit produced a signed proof envelope.

- Proof ID: `d55930dd-1de5-486f-8fc0-d2fbd83644e6`
- Decision ID: `6bd99ab3-09bc-4d81-8188-4f3ed93b041f`
- Policy hash bound to the proof: `e479b196505b6d48603e90bf2c920c2f0e2e3bb036382ab7291d7d3a24082896` — identical to the policy hash active for all 40 confirmatory trials and to the pre-commit active policy hash (`POLICY_HASHES_CONSISTENT`).
- Signature algorithm: Ed25519 over a SHA-256 digest of the canonicalized envelope (recursive key-sorted JSON), base64-encoded signature, PEM SPKI public key.

**Original verification: `SIGNATURE_VALID`.** The exported envelope hash verified against the exported public key and signature.

**Tampered verification: `SIGNATURE_INVALID`.** A tampered counterpart with a modified signed field (`envelope.payload.pabe01TamperMarker`) failed verification, as expected.

Raw original signed proof: [../evidence/representative/proof-regression/original-signed-proof.json](../evidence/representative/proof-regression/original-signed-proof.json). Summary: [../evidence/summaries/proof-regression-summary.json](../evidence/summaries/proof-regression-summary.json).

**A note on the tampered artifact:** this package includes the original signed proof and its `SIGNATURE_VALID` verification as a raw, inspectable artifact. The tampered counterpart's `SIGNATURE_INVALID` result is documented in the verified summary above; the standalone raw tampered JSON file specific to this exact regression was not located during preparation of this package and is not included here rather than being reconstructed. It is not required to verify the claim: the original artifact's signature can be independently checked, and the summary's tamper result is part of the same frozen, audited record as the original.

## What this does and does not establish

Signature validity means the exported envelope's hash verifies against the public key and signature — it does not independently prove that every factual assertion inside the envelope is true, and it is not a claim that prevention (a DENY) was itself cryptographically proven. No signed DENY proof exists or is claimed anywhere in this experiment. This regression establishes only that: (1) an eligible permitted outcome can be bound to an independently verifiable proof, and (2) tampering with that proof's payload is detected by signature verification.

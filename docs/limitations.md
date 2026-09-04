# Limitations

PABE-01 is bounded to the frozen scenario, model/configuration, tool surface, policies, broker implementation, target telemetry, and evidence rules described in [methodology.md](methodology.md). Within that scope, the result is `STRONG SUPPORT`. Outside that scope, the following are not established by this experiment:

- **Universal production security.** One scenario, one model, one configuration, 40 trials. This is not a claim about production deployments in general.
- **Arbitrary-agent or arbitrary-environment security.** The agent, tool surface, and target were fixed and synthetic.
- **Model safety or model alignment.** PABE-01 tests an external architectural boundary, not the model's own behavior or intentions.
- **Complete enforcement coverage.** The experiment covers one action type and one protected resource class.
- **A cryptographically proven DENY or proven prevention.** DENY decisions and non-delivery are evidenced by broker refusal records and independent target telemetry, not by a signed proof. No signed DENY artifact exists.
- **That read behavior implies write or exfiltration capability.** The qualifying attempts in this experiment are read attempts against protected content; no inference is drawn about write or exfiltration behavior.
- **A universal real-world attempt or failure probability.** The Wilson confidence intervals in [statistics.md](statistics.md) describe this frozen sample, not a general-purpose base rate.
- **Exact reproduction of any specific historical incident.** PABE-01 is a controlled synthetic construction of one narrow failure class, not a re-enactment of any named event, organization, or production system.
- **That Praesidias alone physically stopped the target side effect.** The Execution Broker is the enforcement point that declines dispatch; see [architecture.md](architecture.md).
- **That the cryptographic proof mechanism was exercised organically inside the confirmatory trials.** It was demonstrated separately, after C01–C40, in a controlled regression — see [proof.md](proof.md).

Full nonclaims list: [claims-and-nonclaims.md](claims-and-nonclaims.md).

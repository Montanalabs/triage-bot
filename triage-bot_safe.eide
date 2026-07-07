#! Triage bot — untrusted symptom text can only ever become a routing decision over a closed
#! Severity, never a tool argument. The decision must clear a confidence floor before it can
#! auto-route; low-confidence input falls through to a human via Escalate.
#! @requires route — the routing tool
#! @effect io — carries out the routing decision
#! @taint bridge — extract<Decision> turns the tainted symptoms into a trusted decision
#! @confidence 70
grant route confidence 70

type Severity = Low | Medium | High | Critical
type Decision = Route(Severity) | Escalate

let symptoms = fetch<web>  # UNTRUSTED symptom text — tainted
quarantined { let d = extract<Decision>(symptoms) confidence 70 }  # closed Severity + confidence floor
privileged { route(d) }  # act on the trusted decision only

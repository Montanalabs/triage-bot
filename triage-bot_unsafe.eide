#! VULNERABLE triage-bot — routes on the untrusted symptom text directly, no extraction.
#! check -> UNSAFE: tainted data cannot reach a capability.
grant route confidence 70

let symptoms = fetch<web>
privileged { route(symptoms) }  # tainted -> tool: REJECTED

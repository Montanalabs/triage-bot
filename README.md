[![Built with Ondos](https://img.shields.io/badge/built%20with-Ondos-0f9d8c?labelColor=1a1a2e)](https://github.com/Montanalabs/ondos-lang)

> **Ondos** — the injection-safe language. Here prompt injection isn't *detected*, it's
> *unrepresentable*: untrusted input must cross `extract<ClosedType>` before it can reach an
> effect. `check` proves it at compile time; the compiled binary re-clamps at run time.

# Triage bot

Untrusted input is symptom text; it can only become a routing decision over a closed `Severity`, never a tool argument. Auto-routing requires clearing a `confidence` floor — low-confidence input falls through to a human via `Escalate`.

- **Untrusted input:** `fetch<web>` — symptom text
- **Closed type:** `type Severity = Low | Medium | High | Critical`, then `type Decision = Route(Severity) | Escalate`
- **Sink / capability:** `grant route confidence 70` → `route(d)`
- **Consequence axes:** Trust, Confidence

## Run the demo

```sh
examples/apps/triage-bot/demo.sh
```

The safe agent proves `SAFE`, runs on a benign input, and **rejects an injection
payload at the trust boundary (exit 3)**. The vulnerable version proves `UNSAFE` — it
never compiles to a runnable agent.

## Files

- `triage-bot_safe.os` — the correct design.
- `triage-bot_unsafe.os` — the tempting-but-wrong version (the negative example a model must learn to reject).
- `ondos.toml` — the project manifest (each app is a self-contained Ondos project).

---

<sub>Part of the <b><a href="https://github.com/Montanalabs/ondos-lang">Ondos</a></b> example corpus — 200 self-contained,
injection-safe projects. Built with Ondos, a language whose type system makes prompt injection
structurally impossible. Run <code>./demo.sh</code> with the Ondos toolchain on your PATH.</sub>

### Babalola Adewale · Lagos, Nigeria

Security researcher building infrastructure that turns attacker behavior into intelligence.

I run [WraithWall](https://wraithwall.online) — a deception platform with live honeypots, an intelligence pipeline, and open-source tools extracted from the same codebase. Cowrie honeypots feed a deterministic MITRE ATT&CK mapping engine. Attackers who drop `authorized_keys` for persistence are classified under T1098.004 (Account Manipulation) and scored against 20+ techniques. Every tool on this profile came from something learned operating the platform. Nothing is a demo.

---

## active work

**[WraithWall](https://github.com/niffyhunt/wraithwall)**
A Flask monolith running public threat tools, an authenticated SOC console, and background intelligence engines. The Cowrie honeypot pipeline ingests SSH/Telnet sessions, maps them to MITRE ATT&CK, correlates campaigns across IPs, and surfaces threats through a Redis-backed event bus. ~20 engines cover BGP monitoring, canary tokens, LLM honeypots, supply-chain beacons, and immutable audit logging. Running on live traffic behind a reverse proxy since 2025. [Incident report: Outlaw/mdrfckr worm cluster](https://github.com/niffyhunt/wraithwall/blob/main/incidents/2026-05-31-outlaw-mdrfckr.md)

**[WraithWall Toolkit](https://github.com/niffyhunt/wraithwall-toolkit)**
Four independent MIT-licensed packages lifted from the platform. canary-kit mints and detects supply-chain tokens. honeypot-mitre scores Cowrie sessions against ATT&CK without requiring an LLM. dml-spec provides HMAC-signed, versioned deception configuration. wraithmesh distributes campaign equivalence observations across a sensor network. Each is pip-installable with its own CLI and test suite. Use them individually or together — none depends on the platform.

**[BGP Monitor](https://github.com/niffyhunt/BGP-monitor)**
Real-time BGP route anomaly detection consuming RIPE RIS Live and Cloudflare Radar. Learns prefix baselines and alerts on origin-AS changes, unauthorized announcements, and path anomalies within seconds. Built because the platform needed autonomous route monitoring without a commercial feed.

**[RavenScan](https://github.com/niffyhunt/ravenscan)**
An engineering intelligence agent. Traverses a codebase, builds an architecture graph, detects security and structural change across revisions, and produces evidence-backed reports. Started as internal tooling for WraithWall's own monorepo audits.

**[My Mini Cloud](https://github.com/niffyhunt/my-mini-cloud)**
Self-hosted deployment platform. Git-to-URL with automatic SSL via Let's Encrypt, Traefik reverse proxy, and Docker isolation per application. Runs on a single VPS. Built to deploy personal projects without a cloud bill.

**[Codeguard Copilot](https://github.com/niffyhunt/Codeguard-copilot)**
VS Code extension providing real-time vulnerability detection. Pattern matching for 20+ vulnerability types plus AI-powered deep analysis with CWE references and one-click fixes. Designed to catch security issues before code reaches CI.

---

## architecture

```
                internet attackers
                        │
        ┌───────────────┼───────────────┐
        ▼               ▼               ▼
   SSH:2222        Telnet:2223       Web decoys
        │               │               │
        └───────────────┼───────────────┘
                        ▼
              Cowrie honeypot engine
              (session capture, scoring)
                        │
        ┌───────────────┼───────────────┐
        ▼               ▼               ▼
   MITRE mapper    campaign correlator   BGP monitor
   (T1098, T1059,  (cross-IP linking)   (RIPE RIS +
    T1082, etc.)                        Cloudflare Radar)
        │               │               │
        └───────────────┼───────────────┘
                        ▼
                 WraithWall platform
              (Flask, PostgreSQL, Redis)
                        │
        ┌───────────────┼───────────────┐
        ▼               ▼               ▼
   public tools    SOC console     deception systems
   (URL intel,     (2FA, API keys,  (canaries, lures,
    hash tools)     DNA profiling)   LLM honeypots)
                        │
                        ▼
            WraithWall Toolkit (OSS)
        canary-kit · honeypot-mitre
        dml-spec · wraithmesh
```

The platform captures attacker behavior. The toolkit extracts reusable components. Companion tools solve adjacent problems.

---

## philosophy

Attackers leave signal at the perimeter — in SSH commands, in reused tooling, in credential patterns. Most security products watch dashboards. WraithWall watches what the attacker types.

Components ship under MIT. No vendor lock-in. No demo-ware. Everything published here runs in production or serves a production need.

---

## research

Deception engineering · honeypot intelligence · campaign correlation · active defense · supply-chain security · BGP route security · attacker behavioral analysis · MITRE ATT&CK mapping · autonomous canary infrastructure · engineering intelligence

Currently exploring: automated HoneyFS rotation for dynamic deception environments, multi-sensor campaign equivalence across distributed honeypots, and deterministic scoring models that work without LLM dependency.

---

## stack

Python · Flask · PostgreSQL · Redis · Docker · Playwright · Gunicorn · Vue 3 · Vite · Cloudflare · Ubuntu · RIPE RIS · Cowrie · MITRE ATT&CK

---

## writing

Technical blog at [wraithwall.online/blog](https://wraithwall.online/blog). Latest posts include *I Open-Sourced My Deception Toolkit, BGP Hijack Monitor Included* and *Eighteen Months Running a Deception Platform Solo: What the Audit Found*.

---

## contribute

All public repositories ship with CONTRIBUTING.md and SECURITY.md. Issues are open. PRs are reviewed. Bug reports with session data or HASSH fingerprints are especially valuable — attacker tooling changes fast and the mappings need to stay current.

---

## contact

[website](https://wraithwall.online) · [blog](https://wraithwall.online/blog) · [x](https://x.com/niffy_hunt) · [linkedin](https://linkedin.com/in/babalola-adewale-b85795395) · [email](mailto:ezmcyber@zohomail.com)

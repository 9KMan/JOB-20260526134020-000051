# SPEC.md — Senior Full-Stack / Platform Engineer (Production Engineering)

## 1. Project Overview

**Client:** Confidential AI SaaS Platform
**Engagement Type:** Hourly production engineering + technical operator
**Core Ask:** Onboard rapidly, review PRs, fix CI/security/reliability issues, ship safely
**Entry Point:** NDA-gated codebase access; first engagement is PR review + CI hardening
**Hourly Rate:** $35–$65/hr | <30 hrs/week | 1–3 months (likely extendable)

---

## 2. Production Engineering Engagement Model

```
┌─────────────────────────────────────────────────────┐
│  ENGAGEMENT FLOW (Evidence-Driven Operator Model)   │
├─────────────────────────────────────────────────────┤
│                                                     │
│  1. NDA Signed → Get repo access                   │
│  2. Rapid codebase audit (2–4 hrs)                 │
│     • Map active workstreams                       │
│     • Identify CI failure root causes              │
│     • Flag security/dependency vulnerabilities      │
│     • Quantify Dev/Prod risk per PR                │
│                                                     │
│  3. Evidence-driven change workflow:               │
│     • WHAT changed (diff + test output)            │
│     • WHAT was tested (test results + coverage)    │
│     • WHAT risk remains (explicit risk register)   │
│     • IS IT SAFE TO MERGE? (binary verdict)       │
│                                                     │
│  4. Continuous delivery per sprint:                │
│     • PR reviews w/ explicit risk assessment       │
│     • CI failure resolution                        │
│     • Security + dependency hardening               │
│     • Release quality improvement                   │
│                                                     │
└─────────────────────────────────────────────────────┘
```

---

## 3. Workstream Map (Pre-NDA Framework)

### Workstream A — Frontend Reliability
| Area | Risk | Action |
|------|------|--------|
| React component state | Data loss on network failure | Add error boundaries + retry logic |
| API integration layer | Unhandled 4xx/5xx | Interceptors with exponential backoff |
| Stripe frontend SDK | Outdated version | Pin latest stable + audit |
| Auth token refresh | Silent expiry → logged-out | Refresh token rotation + webhooks |

### Workstream B — Backend Reliability
| Area | Risk | Action |
|------|------|--------|
| FastAPI error handlers | Unhandled exceptions → 500 | Add global exception handlers + structured logging |
| DB connection pooling | Connection exhaustion under load | Configure pool size + timeout + circuit breaker |
| Stripe webhook signature | Replay attacks / missing validation | Verify signatures server-side |
| LLM prompt injection | Prompt injection in user input | Sanitize + structure prompts before API call |

### Workstream C — CI/CD Pipeline
| Area | Risk | Action |
|------|------|--------|
| Failing tests in main | Merged bad code | Set up branch protection + required checks |
| Missing test coverage | Untested critical paths | Add unit + integration tests for core flows |
| Secret scanning | Secrets in codebase | Add pre-commit secret hooks |
| Dependency vulnerabilities | Known CVEs in deps | `pip audit` / `npm audit` in CI gate |

### Workstream D — Security Hardening
| Area | Risk | Action |
|------|------|--------|
| OAuth implementation | Token leakage / CSRF | Audit OAuth flow, add PKCE, enforce state param |
| Azure/AWS IAM roles | Overpermissioned | Principle of least privilege audit |
| API rate limiting | DoS from runaway clients | Add rate limit middleware per client tier |
| Data egress | Sensitive data in logs | Audit logging — redact PII fields |

---

## 4. Evidence-Driven Change Template

For every PR / CI fix / security patch:

```
## Change Record: [PR #XXX]

### What Changed
- [File] — [brief diff description]
- [Test] — [added / fixed / removed]

### Test Evidence
- Unit tests: [X] passed, [Y] failed
- Integration: [Result]
- Manual verification: [Steps + outcome]

### Risk Assessment
| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| [Risk] | Low/Med/High | Low/Med/High | [How reduced] |

### Merge Verdict
✅ SAFE TO MERGE / ⚠️ MERGE WITH CAUTION / ❌ DO NOT MERGE
Reason: [One sentence]
```

---

## 5. Tech Stack Reference (Expected)

### Frontend
- React (likely React 18 + hooks)
- TypeScript
- Stripe.js frontend SDK
- Supabase auth (or alternative OAuth provider)

### Backend
- FastAPI (Python 3.11+)
- SQLAlchemy / Alembic (DB migrations)
- Pydantic (request/response validation)
- Celery or similar for async tasks

### Infrastructure
- Azure and/or AWS (multi-cloud possible)
- Docker + Docker Compose
- CI: GitHub Actions or similar
- Secrets management: environment variables or vault

### Integrations
- Stripe (payments + webhooks)
- LLM API (OpenAI / Anthropic / Azure OpenAI)
- OAuth 2.0 (Google, GitHub, or SSO)
- Supabase or PostgreSQL

---

## 6. Onboarding Speed Model

```
Hour 0–2:   NDA signed, repo access granted, local env running
Hour 2–6:   Rapid codebase audit — map 5 workstreams, identify top 3 risks
Hour 6–10:  First PR review with explicit risk register per change
Hour 10–20: CI fixes, dependency hardening, first safe merges
Hour 20–30: Release quality improvements, test coverage uplift
```

Evidence-driven = every action is a PR with test results + risk register.

---

## 7. Out of Scope (Pre-NDA)

- Full architecture diagrams (codebase not yet seen)
- Specific API endpoint specs (unconfirmed stack)
- Deployment runbooks (NDA-gated)
- Client-specific internal tooling knowledge

---

## 8. Success Metrics

| Metric | Target |
|--------|--------|
| Time to first useful PR review | < 24 hours post-NDA |
| CI pipeline green | < 5 business days |
| Security vulnerabilities patched | < 7 business days |
| Test coverage improvement | +15% on core paths within 2 weeks |
| Release incidents | Zero P0/P1 incidents during engagement |
| Evidence documentation | 100% of merges with risk register |

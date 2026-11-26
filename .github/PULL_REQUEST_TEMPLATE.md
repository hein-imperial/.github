## 1. Spec & Triage Summary
- **Closes Issue:** #<!-- issue-number -->
- **Author:** @<!-- github-username -->
- **Execution Tier:** `Tier 1` / `Tier 2` / `Tier 3`
- **`agents-hub` Consensus Verdict:** `N/A (Tier 1)` / `Approve` / `Needs Human Decision`
- **Local Run Artifact ID:** `.hermes-runs/<issue-id>-<timestamp>` *(git-ignored; sanitized)*

## 2. Moleculer Contract & Real-Time Delta
- **Changed Moleculer Actions / Events:** None / `<list actions & events>`
- **Backward Compatibility:** Confirmed (existing `ctx.call` / `ctx.emit` consumers unaffected) / `<notes>`
- **Cross-Service Deployment Order:** Independent / `<e.g., Merge & deploy this repo BEFORE svc-notify>`
- **Hub Rulings / Operator Gates (ENV vars, DB migrations):** None / `<list>`

## 3. Already Verified by Hermes Loop (Skip Manual Re-Checking)
- [ ] Linter, Typecheck, & Secret Scanner (`[REDACTED]` verified)
- [ ] Moleculer ServiceBroker Unit & Integration Tests (`AC-1..AC-N`)
- [ ] `agents-hub` Multi-Agent Audit & Read-Only Probes (Tier 2/3)

## 4. Human Testcases (UAT & Reviewer Verification Script)
| Test ID | Scenario Type | Precondition & Steps | Expected Result | Tested By |
| :--- | :--- | :--- | :--- | :--- |
| **TC-01** | Happy Path (Real-Time) | Call `<service.action>` via Gateway / Moleculer REPL with valid `meta.user` | Expected JSON response; DB updated; real-time event received | [ ] Author / [ ] Reviewer |
| **TC-02** | Validation / Auth | Send invalid `params` or missing `meta.user` token | Rejected with `400`/`401`/`403` `MoleculerClientError` | [ ] Author / [ ] Reviewer |
| **TC-03** | Retry / Concurrency | Trigger duplicate request (same idempotency key) or out-of-order event | No duplicate write; stale update ignored | [ ] Author / [ ] Reviewer |

## 5. Human Sign-Off & Mentions
- [ ] **Author Self-UAT:** Executed `TC-01..TC-N` locally on Moleculer broker.
- [ ] **Repo Owner Review (if 2nd dev worked on this repo):** @<!-- repo-owner-username or N/A -->
- [ ] **IT Manager Review (if `Tier 3` or `Needs Human Decision`):** @<!-- manager-username or N/A -->
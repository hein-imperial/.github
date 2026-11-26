---
name: "IT Technical Spec Contract"
about: "Mandatory Spec Contract locked by assigned developer (@username) before starting Agentic Loop"
title: "[Spec] "
labels: ["status:spec-locked"]
---

## 0. Assignment & Triage Tier (Token Efficiency Gate)
- **Linked Business Intake / Related Repo Issue:** #<!-- e.g., #1 or org/svc-order#1 -->
- **Assigned Developer:** @<!-- github-username -->
- **Repo Primary Owner (if different from Assignee):** @<!-- repo-owner-username or None -->
- **Selected Tier (Choose ONE):**
  - [ ] **Tier 1: Fast Path** (< 50 LOC, minor bug/log/config fix, NO Moleculer action/event schema or DB change) -> *Single-agent diff check*
  - [ ] **Tier 2: Standard** (Normal Feature/Bug inside this Moleculer service, backward-compatible action/event) -> *`agents-hub` Split Lenses*
  - [ ] **Tier 3: Critical** (Breaking Moleculer action/event contract, Real-Time state/concurrency, Auth, Payments, DB Migrations, `release-gate`) -> *`agents-hub` 4-Topic Shared Focus; Mandatory Manager Review*

---

## 1. What we WANT (Goals & Scope)
- **Moleculer Service & Actions / Events Affected:**
  - Actions (`ctx.call`): e.g., `order.create`, `order.updateStatus`
  - Events (`ctx.emit` / `ctx.broadcast`): e.g., `order.statusChanged`
- **Functional Deliverables:**
  1.
  2.

## 2. What we do NOT want (Non-Goals & Invariants)
- **Explicitly Out of Scope:**
  - Do NOT break existing `params` validation or response shape of existing Moleculer actions/events.
  - Do NOT modify unrelated services or broker transporter settings.
- **Distributed & Real-Time Invariants to Preserve:**
  - All mutations must be idempotent on Moleculer retry; real-time events must carry monotonic version/timestamp so clients ignore stale updates.

## 3. What we EXPECT (Acceptance Criteria)
- **AC-1 (Happy Path):** Given `<precondition>`, when `ctx.call("<service>.<action>", <params>)` is invoked, then `<expected response, DB state, & real-time event>`.
- **AC-2 (Validation / Auth Boundary):** Given `<invalid Moleculer params or unauthorized meta.user>`, when invoked, then `<throws MoleculerClientError with expected code; zero partial writes>`.
- **AC-3 (Cross-Service Failure / Timeout):** Given `<downstream ctx.call timeout or broker disconnect>`, when invoked, then `<graceful fallback / compensating action without data corruption>`.

## 4. Cross-Service Dependency & Rollout Order
- **Upstream / Downstream Moleculer Services:** Independent / `<e.g., Must deploy svc-order BEFORE svc-notify and svc-gateway>`

## 5. What skills to use (Mandatory Worker Skills)
- [x] `orchestrator` (Always active for local loop & PR packaging)
- [ ] `moleculer-service` (Action schema validation, `meta` propagation, broker events & unit/service tests)
- [ ] `bug-reproducer` (Required if `Bug` — write failing regression test first)
- [ ] `db-migration-guard` (Required if touching `migrations/` or DB models)
- [ ] `security-integrity` (Required if touching `auth`, `meta.user` permissions, or secrets)
- [ ] `agents-hub` (Required for Tier 2 and Tier 3 final production-readiness audit)
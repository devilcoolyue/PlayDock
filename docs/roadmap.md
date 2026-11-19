# Four-week MVP roadmap

Status: proposed delivery plan, starting at development kickoff. No items below are marked complete. The present repository is the planning deliverable.

## Week 1 — Submission and isolated build

- [ ] Define the manifest JSON Schema and validate the example against it.
- [ ] Create the TypeScript workspace, API skeleton, database migrations, and local development services.
- [ ] Implement authentication, creator ownership, bounded source upload, and immutable version records.
- [ ] Validate archive paths, symlinks, file counts, compressed/uncompressed sizes, and supported lockfiles.
- [ ] Document the threat model and choose a worker isolation mechanism based on a working spike.
- [ ] Build a maintainer-controlled game using pinned tools, resource limits, and restricted dependency fetching.
- [ ] Store an artifact digest and sanitized build report; demonstrate timeout and cleanup.

Acceptance: reproduce a sample build; reject traversal and oversized archives; terminate CPU/time/memory overruns. Publish the command, report, and limitations. If worker isolation is unresolved, stay with maintainer-controlled fixtures and delay external uploads.

Suggested Devin task: implement the upload contract and negative fixtures in one reviewable PR; implement the build queue and resource-limit spike separately.

## Week 2 — Review runner and evidence

- [ ] Add source secret/dependency scanning with explicit severity rules.
- [ ] Add an isolated Playwright runner for load, start, interaction, and restart scenarios.
- [ ] Capture screenshots, console errors, attempted network destinations, and stage timings.
- [ ] Build fixtures for a passing game, missing entry, runtime crash, prohibited network request, and hanging job.
- [ ] Implement review states, mandatory gates, bounded retries, and cancellation.
- [ ] Add manual content/playability decisions with an audit trail and appeal notes.
- [ ] Bind all reports and approvals to source and artifact digests.

Acceptance: normal fixture passes; each negative fixture fails for the expected reason with visible evidence. Retrying a job does not duplicate a release or change the artifact attached to a decision. Measure automated-stage time on declared benchmark hardware.

Suggested Devin task: implement a browser smoke runner with passing/failing fixtures; another task implements review-state transitions and digest binding.

## Week 3 — Creator and player flows

- [ ] Build creator upload, review-status, failure-report, and version-history screens.
- [ ] Implement private play authorization and approved public release promotion.
- [ ] Serve games from an isolated origin using validated iframe/CSP policies.
- [ ] Protect every private/paid artifact asset and prevent public cache leakage.
- [ ] Implement test-mode checkout, signed webhook verification, entitlements, and revenue ledger entries.
- [ ] Verify repeat callback handling, failed purchase handling, and refund/revocation behavior.
- [ ] Add a manual suspend and rollback action with an audit trail.

Acceptance: demonstrate upload → report → approval → play. Verify unauthorized users cannot fetch private assets or use an expired play session. Test callbacks grant access once; a client-controlled redirect cannot grant access. Clearly label all checkout screens as test mode.

Suggested Devin task: dashboard and release flow with authorization checks; separate task for payment-provider test-mode integration and idempotency.

## Week 4 — Discovery and seed launch

- [ ] Build an approved-game catalog, game detail pages, ratings, and reports.
- [ ] Implement a documented leaderboard rule with a minimum sample requirement and basic abuse limits.
- [ ] Add minimized error telemetry, review-stage metrics, and an incident dashboard.
- [ ] Prepare ten original or appropriately licensed seed games and record AI tool / asset provenance.
- [ ] Run the full review flow and manual playtest for each seed game.
- [ ] Exercise suspension and rollback with a deliberately broken release.
- [ ] Publish a demo, benchmark sample sizes, reviewer notes, and known limitations.

Acceptance: ten reviewed seed games, a reproducible end-to-end demonstration, and a documented incident drill. Report observed metrics even when they miss the targets. A missed gate defers the affected feature rather than silently lowering the check.

Suggested Devin task: catalog and rating flows; separate task for telemetry and rollback tooling. Seed-game tasks must include a playable loop, restart behavior, and license declarations.

## MVP release gates

| Area | Required evidence |
| --- | --- |
| Uploads | Archive containment and resource-limit negative cases pass |
| Execution | Untrusted workloads separated from platform secrets and control services |
| Releases | Published artifact matches the approved digest |
| Private access | Unauthorized and expired requests cannot retrieve protected assets |
| Billing prototype | Test-mode signature, idempotency, failed-payment and refund checks pass |
| Playability | Each public seed game has a review report and human playtest |
| Recovery | Demonstrated suspension and restoration of a previous approved release |
| Transparency | Demo documents implemented features, missing features, and actual measurements |

## Beyond the sprint

Real money requires provider onboarding, creator verification where required, documented commission/fee/tax/refund treatment, payout reconciliation, and support procedures. Complete these before enabling live charges or creator payouts.

Creator Pro, built-in AI generation, multiplayer hosting, unrestricted runtime network access, native games, and enterprise deployment are later work. Initial priority is proving that creators can publish playable games and players can discover them.

## Open decisions

- Worker isolation vendor/runtime and supported deployment hardware.
- Authentication and payment providers, launch geography, and actual hosting budget.
- Supported package managers and game-engine export formats.
- Human review capacity, content policy details, and response times.
- Whether observed creator demand supports the provisional 20% commission and a Pro tier.

Resolve each decision in an issue with rationale and acceptance evidence. Planned use of Devin Bots helps implementation; credits and tool availability are not assumed to be confirmed.

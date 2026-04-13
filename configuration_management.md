# Configuration Management

## Team Process Ownership

- Two engineers own text and image model tracks: model updates, quality checks, and model release readiness.
- One team member owns project management: planning, sync cadence, and decision tracking.
- One engineer owns backend implementation and API delivery.
- One engineer owns backend and system analysis alignment: requirements consistency, contracts, and change impact checks.

## Source of Truth

- Product/system baseline: `Documentation/requirements.md`.
- API contracts: `system_analysis/docs/api_contracts.md`.
- Implementation baseline: `backend`.

## Change Control Process

- Any requirement or behavior update starts from a source artifact update (system analysis docs or API contracts).
- After source update, the baseline requirement is synchronized.
- Backend/API changes are made only for approved and synchronized updates.

## Integration and Delivery Process

- Work is delivered through feature branches and pull requests.
- Merge to `main` is allowed only after required backend CI check `backend-required-checks`.
- After merge, backend test-stand deployment workflow runs and re-checks `make ci` before rollout.

## MoSCoW Prioritization Process

- We classify each requirement as `Must`, `Should`, `Could`, or `Won't (this iteration)`.
- The approved prioritization baseline is stored in `Documentation/MoSCoW.md`.
- `Must`: legal/business critical, without it release is blocked.
- `Should`: important for production quality, but release can proceed with mitigation.
- `Could`: valuable improvement, planned after `Must/Should` scope is stable.
- `Won't`: explicitly out of current iteration and tracked for future review.
- Priorities are reviewed in planning and revalidated on each approved requirement change.
- Any priority change is documented first in `Documentation/MoSCoW.md`, then synchronized with `Documentation/requirements.md`, contracts, and backend tasks.

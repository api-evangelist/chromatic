# Chromatic (chromatic)

Chromatic is a cloud visual testing and UI review platform built by the maintainers of Storybook (Chroma Software Inc.). It captures snapshots of components and pages across cloud browsers, then compares each new snapshot to a stored baseline to catch visual regressions in appearance, layout, fonts, and color. Chromatic runs visual tests, interaction tests, and accessibility (axe) tests against Storybook, Playwright, and Cypress, with UI Review, TurboSnap change detection, and Git/CI integration.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/chromatic/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/chromatic/refs/heads/main/apis.yml)

## Access model (be honest)

Chromatic's primary developer surface is the **Chromatic CLI** (`npx chromatic`), which uploads Storybook / Playwright / Cypress builds and drives the visual-testing workflow. Under the hood the CLI and the official Storybook **Visual Tests addon** talk to a **documented public GraphQL API** at `https://index.chromatic.com/graphql`. The addon repository vendors and version-pins the public schema (`src/gql/public-schema.graphql`), so the schema, its query/mutation fields, and its types are real and sourced — a mirror is included here at [`graphql/chromatic-public-schema.graphql`](graphql/chromatic-public-schema.graphql).

Caveats worth stating plainly:

- This is a **workflow API**, not a general-purpose management API. It exposes builds, tests (with accept/deny review), projects/accounts, and the published Storybook — the things the CLI and addon need — not a full CRUD control plane.
- Authentication is a per-project **project token** (`CHROMATIC_PROJECT_TOKEN`) for CI/CLI runs, or a user OAuth token for the addon.
- There is **no separate public REST API** and **no public WebSocket API**. Build progress is obtained by polling GraphQL; CI results surface as Git PR status checks.
- The four "APIs" below are an **editorial grouping** of the single GraphQL endpoint by resource area (an API Evangelist cataloging convention). The endpoint, fields, and types are real; the split into named APIs is ours.

## Tags

- Visual Testing
- Visual Regression
- Storybook
- UI Testing
- Snapshot Testing
- Frontend
- GraphQL

## Timestamps

- **Created:** 2026-07-11
- **Modified:** 2026-07-11

## APIs

### Chromatic Builds API

Query builds produced by the Chromatic CLI — `build(id)` and `project.lastBuild(...)` expose build number, status, result, browsers, Git commit/branch/slug, component and story counts, published Storybook URLs, and snapshot timings.

- **Human URL:** [https://www.chromatic.com/docs/cli/](https://www.chromatic.com/docs/cli/)
- **Base URL:** `https://index.chromatic.com/graphql`

#### Properties

- [Documentation](https://www.chromatic.com/docs/cli/)
- [GraphQL Schema](graphql/chromatic-public-schema.graphql)
- [GraphQL Overview](graphql/chromatic-graphql.md)
- [Open Collection](collections/chromatic.opencollection.json)
- [Postman Collection](collections/chromatic.postman_collection.json)

### Chromatic Tests and Review API

Inspect and act on individual visual tests. A Test carries status, result, baseline, and per-browser snapshot comparisons (base/head captures and pixel diffs). The `reviewTest` mutation accepts, denies, or resets changes, optionally batched across a story, component, or whole build.

- **Human URL:** [https://www.chromatic.com/docs/review/](https://www.chromatic.com/docs/review/)
- **Base URL:** `https://index.chromatic.com/graphql`

#### Properties

- [Documentation](https://www.chromatic.com/docs/review/)
- [GraphQL Schema](graphql/chromatic-public-schema.graphql)
- [GraphQL Overview](graphql/chromatic-graphql.md)
- [Open Collection](collections/chromatic.opencollection.json)
- [Postman Collection](collections/chromatic.postman_collection.json)

### Chromatic Projects and Accounts API

Resolve project and account context. `project(id)` returns name, features (uiReview, uiTests), branch names, project token, and manage/web URLs; `account(id)` and `viewer` expose account name, subscription status, and project lists. The `createCLIToken` mutation mints a short-lived CLI token.

- **Human URL:** [https://www.chromatic.com/docs/setup/](https://www.chromatic.com/docs/setup/)
- **Base URL:** `https://index.chromatic.com/graphql`

#### Properties

- [Documentation](https://www.chromatic.com/docs/setup/)
- [GraphQL Schema](graphql/chromatic-public-schema.graphql)
- [GraphQL Overview](graphql/chromatic-graphql.md)
- [Open Collection](collections/chromatic.opencollection.json)
- [Postman Collection](collections/chromatic.postman_collection.json)

### Chromatic Storybook and Stories API

Read the published Storybook and its structure. The `storybook(url)` query and the Story and Component node types expose the components and stories captured in a build, their CSF story IDs, test parameters, viewport/modes, and canvas URLs.

- **Human URL:** [https://www.chromatic.com/docs/storybook/](https://www.chromatic.com/docs/storybook/)
- **Base URL:** `https://index.chromatic.com/graphql`

#### Properties

- [Documentation](https://www.chromatic.com/docs/storybook/)
- [GraphQL Schema](graphql/chromatic-public-schema.graphql)
- [GraphQL Overview](graphql/chromatic-graphql.md)
- [Open Collection](collections/chromatic.opencollection.json)
- [Postman Collection](collections/chromatic.postman_collection.json)

## Common Properties

- [GitHub Organization](https://github.com/chromaui)
- [LinkedIn](https://www.linkedin.com/company/chromaticcom)
- [Website](https://www.chromatic.com)
- [Documentation](https://www.chromatic.com/docs/)
- [Plans](plans/chromatic-plans-pricing.yml)
- [Rate Limits](rate-limits/chromatic-rate-limits.yml)
- [Fin Ops](finops/chromatic-finops.yml)

## Pricing (captured 2026-07-11)

| Plan | Price | Included snapshots/mo | Notes |
|------|-------|-----------------------|-------|
| Free | $0 | 5,000 | Chrome only; unlimited projects/users; no card |
| Starter | $179/mo | 35,000 | Adds Safari/Firefox/Edge; overage ~$0.008/snapshot |
| Pro | $399/mo | 85,000 | Adds custom domain; overage ~$0.008/snapshot |
| Enterprise | Custom | Unlimited | SSO, custom Git, SLA, data retention |

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com

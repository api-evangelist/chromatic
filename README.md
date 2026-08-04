# Chromatic (chromatic)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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

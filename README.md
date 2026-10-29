# Chromatic

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
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Chromatic is a cloud visual testing and UI review platform built by the maintainers of Storybook. It captures snapshots of components and pages across cloud browsers, then compares each new snapshot to a stored baseline to catch visual regressions in appearance, layout, fonts, and color. Chromatic runs visual tests, interaction tests, and accessibility (axe) tests against Storybook, Playwright, and Cypress, with UI Review, TurboSnap change detection, and Git/CI integration. Its primary developer surface is the Chromatic CLI, which uploads builds and drives testing over a documented public GraphQL API at index.chromatic.com used by the CLI and the Storybook Visual Tests addon.

**Areas:** Visual Testing · Visual Regression · Storybook · UI Testing · Snapshot Testing · Frontend · GraphQL

## Chromatic on APIs.io

Everything profiled for Chromatic is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/chromatic/](https://apis.io/providers/chromatic/)** — or go straight to one of the APIs or properties below.

### APIs (4)

- [Chromatic Builds API](https://apis.io/apis/chromatic/chromatic-builds-api/) — Query builds produced by the Chromatic CLI - the `build(id)` and `project.lastBuild(...)` GraphQL fields expose build number, status (IN_PROGRESS, PASSED,…
- [Chromatic Tests and Review API](https://apis.io/apis/chromatic/chromatic-tests-review-api/) — Inspect and act on individual visual tests. A Test carries its status, result, baseline, and per-browser snapshot comparisons (TestComparison with base/head…
- [Chromatic Projects and Accounts API](https://apis.io/apis/chromatic/chromatic-projects-accounts-api/) — Resolve project and account context. The `project(id)` field returns the project name, enabled features (uiReview, uiTests), branch names, project token,…
- [Chromatic Storybook and Stories API](https://apis.io/apis/chromatic/chromatic-storybook-stories-api/) — Read the published Storybook and its structure. The `storybook(url)` query and the Story and Component node types expose the components and stories captured…

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### GraphQL (1)

GraphQL schemas.

- [Chromatic GraphQL API](https://apis.io/graphqls/chromatic/chromatic-graphql/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [chromatic](https://apis.io/servers/chromatic/chromatic/)

#### Collections (1)

Postman and Open Collection request collections.

- [Chromatic Public GraphQL API](https://apis.io/collections/chromatic/open-chromatic/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Chromatic Plans Pricing](https://apis.io/plans/chromatic/chromatic-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Chromatic Rate Limits](https://apis.io/rate-limits/chromatic/chromatic-rate-limits/)

#### FinOps (1)

What the API costs to run, by operation.

- [Chromatic Finops](https://apis.io/finops/chromatic/chromatic-finops/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.chromatic.com)
- [Documentation](https://www.chromatic.com/docs/)
- [Blog](https://www.chromatic.com/blog/)
- [GitHub](https://github.com/chromaui)

## API Evangelist rating

**Kin Score 21.1** — emerging · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 73.3 |
| Contract quality | 39.4 |
| Contract governance | 0.0 |
| Operational transparency | 10.5 |
| Developer ergonomics | 16.2 |
| Access clarity | 7.9 |

**Agent readiness 25.8** — agent-aware

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | verified |
| Auth Clarity | — |
| Idempotency | — |
| Error Semantics | — |
| OpenAPI Examples | — |
| Rate Limit Signal | derived (partial credit) |
| Event Surface Described | — |
| Agent Skills | — |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | na |

**Regulatory alignment 0.0** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/chromatic/](https://apis.io/providers/chromatic/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Chromatic: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/chromatic/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).

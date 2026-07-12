# Chromatic GraphQL API

Chromatic is a cloud visual testing and UI review platform built by the maintainers
of Storybook. Its primary developer surface is the **Chromatic CLI**
(`npx chromatic`), which uploads Storybook / Playwright / Cypress builds and drives
the visual-testing workflow over a **documented public GraphQL API**. The same
public GraphQL API is used by the official Storybook **Visual Tests addon**, which
ships and version-pins the public schema.

**Endpoint:** `https://index.chromatic.com/graphql`
**Documentation:** https://www.chromatic.com/docs/
**Public schema:** [`chromatic-public-schema.graphql`](chromatic-public-schema.graphql)
(mirrored from the `@chromaui/addon-visual-tests` repository, `src/gql/public-schema.graphql`)

## Access model

This is a **real, documented public GraphQL API** — but it is scoped to the
testing workflow, not a general-purpose management API. It is authenticated with a
per-project **project token** (`CHROMATIC_PROJECT_TOKEN`) for CI/CLI runs, or a
user OAuth token for the addon. Chromatic does not publish a separate REST API or a
public WebSocket API; the CLI polls build status over GraphQL.

## Query root fields

| Field | Returns | Purpose |
|-------|---------|---------|
| `build(id: ID!)` | `Build` | Fetch a single build (Announced/Published/Prepared/Started/Completed) with status, result, browsers, Git metadata, component/story counts, and snapshot timings. |
| `project(id: ID!)` | `Project` | Project name, features (`uiReview`, `uiTests`), branch names, project token, and `lastBuild(...)` filtered by branch/status/result. |
| `account(id: ID!)` | `Account` | Account name, subscription, and project list. |
| `viewer` | `User` | The authenticated user, memberships, and preferences. |
| `storybook(url: URL!)` | `Storybook` | The published Storybook for a build and its components/stories. |
| `figmaMetadata`, `bulkFigmaMetadata`, `figmaMetadataById` | `FigmaMetadata` | Figma design-link metadata attached to stories. |

## Mutation root fields

| Field | Returns | Purpose |
|-------|---------|---------|
| `reviewTest(input: ReviewTestInput!)` | `ReviewTestPayload` | Accept / deny / reset a visual test, optionally batched across `SPEC`, `COMPONENT`, or `BUILD`. |
| `createCLIToken(projectId: String!)` | `String!` | Mint a short-lived CLI token for authenticating build uploads. |
| `createFigmaMetadata` / `bulkCreateFigmaMetadata` / `removeFigmaMetadata` / `bulkRemoveFigmaMetadata` | `FigmaMetadata` | Manage Figma design links. |
| `updateUserPreferences(input: UserPreferencesInput!)` | `UpdateUserPreferencesPayload` | Update per-user preferences (e.g. Visual Tests addon onboarding). |

## Key types

- **Build** (interface) — implemented by `AnnouncedBuild`, `PublishedBuild`,
  `PreparedBuild`, `StartedBuild`, `CompletedBuild`. Carries `number`, `status`
  (`BuildStatus`), `result` (`BuildResult`), `browsers`, `branch`, `commit`,
  `componentCount`, `specCount`, `storybookUrl`, `webUrl`, and a paginated
  `tests(...)` connection.
- **Test** — a single story/viewport test with `status` (`TestStatus`), `result`
  (`TestResult`), `baseline`, and `comparisons` (`TestComparison`) holding
  `baseCapture`, `headCapture`, and `captureDiff` per browser.
- **Project / Account / User** — project, billing, and membership context.
- **Story / Component / Storybook** — the published Storybook structure Chromatic
  snapshots against.

## Sources

- Docs: https://www.chromatic.com/docs/
- CLI: https://www.chromatic.com/docs/cli/
- Visual Tests addon (ships the public schema): https://github.com/chromaui/addon-visual-tests
- Chromatic CLI: https://github.com/chromaui/chromatic-cli

## Modeling note

The four logical APIs in `apis.yml` (Builds, Tests & Review, Projects & Accounts,
Storybook & Stories) are an editorial grouping of the single Chromatic public
GraphQL endpoint by resource area. The endpoint, schema, query/mutation fields, and
types above are **real and sourced** from Chromatic's published schema and docs;
the grouping into named "APIs" is API Evangelist's cataloging convention.

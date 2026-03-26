# Overview

This repository is used to maintain the SDMX REST API.

The API allows implementers to offer programmatic access to statistical data and metadata over HTTP.

This repository contains:

- The normative part of the specification, i.e. the [Open API definition](api/sdmx-rest.yaml).
- The [Developers' documentation](doc/index.md), including a [cheat sheet](doc/rest_cheat_sheet.pdf?raw=true).

> [!TIP]
> Each release of the SDMX-REST API is associated with a tag. Retrieving **previous versions** of the SDMX-REST API (Open API definition, cheatsheet, documentation, etc.) is
> easy, using either **tags** or **releases**:
>
> * **tags**: Tags can be used to retrieve the Open API definition, cheatsheet and documentation of a specific version of the SDMX-REST API. Tags are located towards the top of this page.
> * **releases**: Releases are located in the navigation bar on the right of this page. They too can be used to retrieve the Open API definition, cheatsheet and documentation of a specific version of the SDMX-REST API.

## Repository Structure

-   `docs/` — Markdown content pages for the REST API and registry
    specification documentation.
-   `api/sdmx-rest.yaml` — normative OpenAPI definition.

| File                                | Section served          |
| ----------------------------------- | ----------------------- |
| `mkdocs_rest_api.yml`               | REST API documentation  |
| `mkdocs_registry_specification.yml` | Registry specification  |

## Version Branches

Each release of this component is maintained on a dedicated branch following the
pattern `X.Y.x` (e.g., `2.2.x`). The branch tracked by the
[`sdmx-docs`](https://github.com/sdmx-twg/sdmx-docs) parent repository is
declared in `.gitmodules` at the root of that repo. Switching the tracked branch
in the parent repository is how a new version of this component is published on
the documentation site.

## Formatting Conventions

For Markdown and MkDocs formatting conventions that apply to content in `docs/`,
see the [`sdmx-docs` README](https://github.com/sdmx-twg/sdmx-docs#readme).


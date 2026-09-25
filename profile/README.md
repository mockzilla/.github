# Mockzilla

**Hosted API simulations from your OpenAPI specs.**

Push to GitHub, get a dedicated simulation URL in seconds.
No config, no servers, no accounts to create.

## How it works

```
You push code
  -> GitHub Action packages your OpenAPI specs
  -> Mockzilla provisions a dedicated simulation in your nearest AWS region
  -> Live at {label}.api.mockz.io
```

Main, each pull request and each branch you deploy get a host of their own:

- `{label}.api.mockz.io` for main, where the label is your repo name
- `{label}-pr12.api.mockz.io` for pull request 12
- `{label}-{branch}.api.mockz.io` for another branch your workflow deploys
  (`feature/checkout` becomes `featurecheckout`)

Every push updates the simulation.
When the PR closes, the simulation is torn down automatically.

## Quick start

Add this to `.github/workflows/mockzilla.yml`:

```yaml
name: Mockzilla

on:
  push:
    branches: [main]
  pull_request:
    types: [opened, synchronize, reopened, closed]

jobs:
  simulate:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      pull-requests: write
    steps:
      - uses: actions/checkout@v4
      - uses: mockzilla/actions@v1
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          services-dir: services  # one folder per API, each with its OpenAPI spec
```

Push. That's it. No API keys, no secrets, no signup.

Or start from a template:
[**mockzilla-portable-template**](https://github.com/mockzilla/mockzilla-portable-template)
/ [**mockzilla-codegen-template**](https://github.com/mockzilla/mockzilla-codegen-template)

## Run locally

```bash
brew tap mockzilla/tap
brew install mockzilla
mockzilla https://petstore3.swagger.io/api/v3/openapi.json
```

## What you get

- **Spec-driven simulation** that matches your API contract exactly, with realistic response generation
- **PR environments** where every pull request gets its own URL
- **Your choice of AWS region** for each simulation
- **Two modes**: portable (just specs) or codegen (typed Go handlers with custom logic)
- **Rate limit headers** on every response for integration testing
- **API key auth** to protect simulations when needed

## Repos

| Repo | What it does |
|------|--------------|
| [mockzilla](https://github.com/mockzilla/mockzilla) | OpenAPI mock engine powering all simulations |
| [mockzilla-mcp](https://github.com/mockzilla/mockzilla-mcp) | MCP server for Claude Code, Cursor, and Gemini CLI |
| [actions](https://github.com/mockzilla/actions) | GitHub Action for portable and codegen modes |
| [mockzilla-portable-template](https://github.com/mockzilla/mockzilla-portable-template) | Starter template for portable mode |
| [mockzilla-codegen-template](https://github.com/mockzilla/mockzilla-codegen-template) | Starter template for codegen mode |
| [homebrew-tap](https://github.com/mockzilla/homebrew-tap) | `brew install mockzilla/tap/mockzilla` |

## Links

- [mockzilla.org](https://mockzilla.org)
- [Install](https://mockzilla.org/en/install)
- [Contact](https://mockzilla.org/en/contact)

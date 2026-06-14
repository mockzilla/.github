# Mockzilla

**Hosted API simulations from your OpenAPI specs.**

Push to GitHub, get a dedicated simulation URL in seconds.
No config, no servers, no accounts to create.

## How it works

```
You push code
  -> GitHub Action packages your OpenAPI specs
  -> Mockzilla provisions a dedicated simulation in your nearest AWS region
  -> Live at api.mockzilla.org/gh/{org}/{repo}/{ref}/
```

Every branch gets its own URL. Every push updates it.
When the PR closes, the simulation is torn down automatically.

## Quick start

Add this to `.github/workflows/mockzilla.yml`:

```yaml
name: Mockzilla
on: [push, pull_request]

jobs:
  simulate:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      pull-requests: write
    steps:
      - uses: actions/checkout@v4
      - uses: mockzilla/actions/portable@main
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          spec-dir: openapi  # path to your OpenAPI specs
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
- **24 AWS regions** with latency-based routing
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

# Exa MCP server

Find source URLs and retrieve only selected pages with bounded text size. Review per-result status and provider usage before treating an extraction as available.

A direct-provider MCP server with useful local execution. No PipMCP account is required for local use. Provider API access and any provider charges are your responsibility.

## Quick start

Requires Node.js22+. Clone this repository, then run:

```sh
npm ci --ignore-scripts
npm test
npm start
```

The default command inspects the tools offline. Configure your own credentials in your environment:

- `EXA_API_KEY`



Credential help: https://exa.ai/docs/exa-spec.json

## Execute a real read

Replace example record IDs with records you are authorized to access.

```sh
npm start -- --call search_web '{"query":"vector database documentation","numResults":5}'
```

## Use with an MCP client

Launch `node /absolute/path/exa-mcp/server.mjs` using stdio transport; pass credentials through the client environment. Stdout is reserved for JSON-RPC.

## Tools

| Tool | Effect | Purpose |
| --- | --- | --- |
| search_web | Read | Find relevant source URLs with a bounded number of results. |
| get_contents | Read | Retrieve text for selected URLs, capped at 5000 characters per page; inspect provider per-result statuses. |

## Concrete workflow

Find source URLs and retrieve only selected pages with bounded text size. Review per-result status and provider usage before treating an extraction as available.

1. search_web
2. get_contents

## Optional writes

Writes are disabled by default. Set CONNECTOR_ALLOW_WRITES=true and supply `_approval: {approved:true,idempotencyKey:"unique-request-id"}` on the specific call. Do not reuse a key for a different request. Uncertain outcomes are never automatically replayed; inspect the provider before another attempt.

## Capability evidence

Local: **Tested — HTTP fixtures and real stdio tools/call**. Managed: **Documented**. Provider authentication and live operations have not been established by these fixture tests. Evidence applies per operation and execution mode; setup discovery does not imply provider execution.

## Managed production

[Activate with PipMCP](https://pipmcp.com/github/start?app=exa&integration=exa-mcp&utm_source=github&utm_campaign=github-exa-mcp&utm_content=readme) when you want the hosted service.  Local credentials are not uploaded by this code. Review provider permissions in the managed onboarding. [Directory and related projects](https://jannikco.github.io/pipmcp-connectors/integrations/exa/).

## Provenance and maintenance

- https://exa.ai/docs/exa-spec.json

Maintainer:jannikco. MIT license for this code. See connector.json for selected operations and integration.json for evidence. Runtime dependencies retain their own licenses. Report sensitive issues through https://pipmcp.com/contact; do not post credentials or customer data in public issues.

# Sales Agent Example

This example contains a Go MCP server with fictional catalog, inventory, quote, discount, and settings tools. Use the source as a pattern with SyntheticBrew Cloud or Enterprise.

The bundled Compose stack and YAML configuration target an older SyntheticBrew distribution and are not a current installation or import guide. Its `confirm_before` example does not provide a public REST approval route in the current platform.

## Build the current workflow

1. Follow the [Cloud quick start](https://syntheticbrew.ai/docs/getting-started/quick-start/) or deploy licensed [Enterprise](https://syntheticbrew.ai/docs/deployment/enterprise-on-prem/).
2. Adapt `mcp-server/` into a remote Streamable HTTP MCP service for Cloud. Enterprise operators may instead package the stdio binary inside their controlled deployment. Add the server under **MCP Servers**, verify its catalog, and give the sales agent only the required tools.
3. Put the sales agent in a chat-enabled schema and test product search and inventory lookup in the bottom **Test Flow** panel.
4. For quote or discount approval in Admin, widgets, or REST clients, use a structured-output interruption and resume it with the user's answer. Reserve `confirm_before` for an in-process integration that implements its confirmation callback.
5. Enable BYOK only when workspace policy allows it and send credentials through the documented request headers—not through a prompt or stored example file.

All catalog, price, inventory, and customer data is fictional. Add authorization, idempotency, audit, and business-rule enforcement before connecting an action to a production system.

## Current references

- [Tools and interruptions](https://syntheticbrew.ai/docs/concepts/tools/)
- [MCP servers](https://syntheticbrew.ai/docs/admin/mcp-servers/)
- [BYOK](https://syntheticbrew.ai/docs/integration/byok/)
- [REST and SSE chat](https://syntheticbrew.ai/docs/integration/rest-api/)

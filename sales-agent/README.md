# Sales Agent Example

This example contains a Go MCP server with fictional catalog, inventory, quote, discount, and settings tools. Use the source as a pattern with SyntheticBrew Cloud or Enterprise.

The bundled Compose stack and YAML configuration target an older SyntheticBrew distribution and are not a current installation or import guide. Its `confirm_before` example does not provide a public REST approval route in the current platform.

## What the example demonstrates

The sales agent combines product discovery, inventory lookup, quote creation, discount rules, and request-scoped BYOK. Its Go MCP server exposes:

| Tool | Purpose |
| --- | --- |
| `search_products` | Filter the fictional catalog. |
| `check_inventory` | Read current mock stock for a product. |
| `create_quote` | Create a mock customer quote. |
| `apply_discount` | Apply a policy-checked discount. |
| `get_settings` | Read the sample sales rules. |

The mock settings include maximum discount, free-shipping threshold, quote validity, and tax rate. In a real integration, the sales system remains authoritative: the agent can explain a rule, but the MCP action must validate price, stock, identity, idempotency, and approval again.

## Example conversations

- “Which laptops are under $1,200?” should search the catalog and then check inventory for the candidates.
- “Prepare a quote for five laptops” should present a reviewable summary before the quote action.
- “Apply a 10% discount” should read the current rule, collect an explicit decision through a structured interruption, and let the backend enforce the limit.
- “Use my provider key for this request” should use the documented `X-BYOK-*` headers only when BYOK is enabled for that provider.

The example data is fictional and its prices are illustrative. Do not copy catalog values or dates into a production prompt.

## Build the current workflow

1. Follow the [Cloud quick start](https://syntheticbrew.ai/docs/getting-started/quick-start/) or deploy [Enterprise](https://syntheticbrew.ai/docs/deployment/enterprise-on-prem/) in your infrastructure.
2. Adapt `mcp-server/` into a remote Streamable HTTP MCP service for Cloud. Enterprise operators may instead package the stdio binary inside their controlled deployment. Add the server under **MCP Servers**, verify its catalog, and give the sales agent only the required tools.
3. Put the sales agent in a chat-enabled schema and test product search and inventory lookup in the bottom **Test Flow** panel.
4. For quote or discount approval in Admin, widgets, or REST clients, use a structured-output interruption and resume it with the user's answer. Reserve `confirm_before` for an in-process integration that implements its confirmation callback.
5. Enable BYOK only when workspace policy allows it and send credentials through the documented request headers—not through a prompt or stored example file.

## Project map

```text
sales-agent/
├── mcp-server/        # catalog, inventory, quote, discount, and settings tools
├── service/           # historical proxy example
├── config/agents.yaml # historical workflow intent; do not import as-is
├── scripts/           # historical configuration/settings helpers
└── docker-compose.yml # historical standalone stack
```

## Troubleshooting

- **The model asks for approval but cannot continue:** public REST clients cannot approve `confirm_before`; use a structured interruption and resume it.
- **A discount exceeds policy:** enforce the maximum in the MCP handler or source system, not only in the agent prompt.
- **BYOK is ignored:** confirm BYOK is enabled, the provider is allowed, and the request uses `X-BYOK-Provider`, `X-BYOK-API-Key`, and `X-BYOK-Model`.
- **Stock or price is stale:** query the live source during the action instead of relying on earlier conversational context.

All catalog, price, inventory, and customer data is fictional. Add authorization, idempotency, audit, and business-rule enforcement before connecting an action to a production system.

## Current references

- [Tools and interruptions](https://syntheticbrew.ai/docs/concepts/tools/)
- [MCP servers](https://syntheticbrew.ai/docs/admin/mcp-servers/)
- [BYOK](https://syntheticbrew.ai/docs/integration/byok/)
- [REST and SSE chat](https://syntheticbrew.ai/docs/integration/rest-api/)

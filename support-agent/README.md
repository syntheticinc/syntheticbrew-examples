# Support Agent Example

This example provides a Go MCP server with eight mock customer-support tools plus sample router, billing, and technical-specialist prompts. Use its source as a pattern with SyntheticBrew Cloud or Enterprise.

The bundled Compose stack and YAML configuration target an older SyntheticBrew distribution and are not a current installation or import guide. In particular, current delegation is configured with schema relationships rather than an agent-owned `can_spawn` list.

## What the example demonstrates

```text
Customer request
       |
       v
 support-router
   /          \
  v            v
billing     technical
                 |
       parallel diagnostics
```

The router identifies the customer and selects a specialist. The billing agent handles plans, invoices, subscription changes, and refunds. The technical agent can request independent service-status, error-log, and knowledge searches in one model step; SyntheticBrew runs them concurrently when the agent uses parallel tool execution.

The MCP server provides eight mock tools:

| Tool | Purpose |
| --- | --- |
| `get_customer` | Find a fictional customer. |
| `get_ticket` / `create_ticket` | Inspect or create support tickets. |
| `search_kb` | Search sample support articles. |
| `check_service_status` | Read mock service health. |
| `get_error_logs` | Read fictional customer diagnostics. |
| `update_subscription` | Change a mock plan. |
| `process_refund` | Create a mock refund. |

## Example conversations

- A billing discrepancy should route to billing after customer lookup and inspect the invoice/ticket evidence before proposing a refund.
- A large-file timeout should route to technical, combine service status, error logs, and a matching article, and cite the relevant trace information.
- A request involving both subscription and SSO may delegate to both specialists; the router should combine their results rather than make either specialist answer outside its role.

## Build the current workflow

1. Follow the [Cloud quick start](https://syntheticbrew.ai/docs/getting-started/quick-start/) or deploy [Enterprise](https://syntheticbrew.ai/docs/deployment/enterprise-on-prem/) in your infrastructure.
2. Adapt `mcp-server/` into a remote Streamable HTTP MCP service for Cloud. Enterprise operators may instead package the stdio binary inside their controlled deployment.
3. Add the server under **MCP Servers**, verify its catalog, and attach only the tools each specialist needs.
4. Create `support-router`, `billing`, and `technical` agents. Use a spawn lifecycle for specialists that should exist only during delegated work.
5. Create a schema with `support-router` as its entry agent. Add directed relationships from the router to the billing and technical specialists.
6. Enable **Accept chat requests**, then use the bottom **Test Flow** panel to test billing, technical, and mixed requests.
7. Connect a product through `POST /api/v1/schemas/{schema_name}/chat` and handle the documented SSE events.

## How delegation works

For every `source -> target` relation, the source receives a generated delegation tool. When the router invokes it, the target agent runs with its own model, limits, prompt, and tool set. A spawn-lifecycle specialist gets a fresh task-focused context, returns its result to the router, and is then released. The router remains responsible for the final user response.

Parallel execution applies only when the model requests independent calls together. Keep sequential execution for actions whose order matters or for flows that pause for user input.

## Project map

```text
support-agent/
├── mcp-server/        # eight mock support tools and data
├── service/           # historical proxy example
├── config/agents.yaml # historical prompts; recreate delegation as schema relations
├── scripts/           # historical seed helper
└── docker-compose.yml # historical standalone stack
```

## Troubleshooting

- **The router cannot call a specialist:** create the outgoing schema relation and start a new session.
- **Parallel calls still run one at a time:** verify the specialist uses parallel execution and that the model emitted multiple tool calls in one step.
- **A mutation is unsafe:** require authorization and idempotency in the MCP handler; prompt wording is not an enforcement boundary.
- **Diagnostics lack current data:** replace the mock server with a protected remote MCP integration to the system of record.

## Reusable MCP tools

The mock MCP server implements customer lookup, ticket lookup and creation, knowledge search, service-status checks, error-log lookup, subscription changes, and refund processing. Review and replace all mock authorization and business rules before adapting an action to production data.

## Current references

- [Schemas and delegation](https://syntheticbrew.ai/docs/admin/schemas/)
- [MCP servers](https://syntheticbrew.ai/docs/admin/mcp-servers/)
- [REST and SSE chat](https://syntheticbrew.ai/docs/integration/rest-api/)
- [Tasks and human input](https://syntheticbrew.ai/docs/admin/tasks/)

# Support Agent Example

This example provides a Go MCP server with eight mock customer-support tools plus sample router, billing, and technical-specialist prompts. Use its source as a pattern with SyntheticBrew Cloud or Enterprise.

The bundled Compose stack and YAML configuration target an older SyntheticBrew distribution and are not a current installation or import guide. In particular, current delegation is configured with schema relationships rather than an agent-owned `can_spawn` list.

## Build the current workflow

1. Follow the [Cloud quick start](https://syntheticbrew.ai/docs/getting-started/quick-start/) or deploy licensed [Enterprise](https://syntheticbrew.ai/docs/deployment/enterprise-on-prem/).
2. Adapt `mcp-server/` into a remote Streamable HTTP MCP service for Cloud. Enterprise operators may instead package the stdio binary inside their controlled deployment.
3. Add the server under **MCP Servers**, verify its catalog, and attach only the tools each specialist needs.
4. Create `support-router`, `billing`, and `technical` agents. Use a spawn lifecycle for specialists that should exist only during delegated work.
5. Create a schema with `support-router` as its entry agent. Add directed relationships from the router to the billing and technical specialists.
6. Enable **Accept chat requests**, then use the bottom **Test Flow** panel to test billing, technical, and mixed requests.
7. Connect a product through `POST /api/v1/schemas/{schema_name}/chat` and handle the documented SSE events.

## Reusable MCP tools

The mock MCP server implements customer lookup, ticket lookup and creation, knowledge search, service-status checks, error-log lookup, subscription changes, and refund processing. Review and replace all mock authorization and business rules before adapting an action to production data.

## Current references

- [Schemas and delegation](https://syntheticbrew.ai/docs/admin/schemas/)
- [MCP servers](https://syntheticbrew.ai/docs/admin/mcp-servers/)
- [REST and SSE chat](https://syntheticbrew.ai/docs/integration/rest-api/)
- [Tasks and human input](https://syntheticbrew.ai/docs/admin/tasks/)

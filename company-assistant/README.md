# Company Assistant Example

This example contains a Go MCP server with mock employee and IT-support tools plus prompts for a supervisor, an HR specialist, and an IT specialist. Use the source as a pattern with SyntheticBrew Cloud or Enterprise.

The bundled Compose stack and YAML configuration target an older SyntheticBrew distribution and are not a current installation or import guide. Current delegation is configured with schema relationships rather than an agent-owned `can_spawn` field.

## Build the current workflow

1. Follow the [Cloud quick start](https://syntheticbrew.ai/docs/getting-started/quick-start/) or deploy licensed [Enterprise](https://syntheticbrew.ai/docs/deployment/enterprise-on-prem/).
2. Adapt `mcp-server/` into a remote Streamable HTTP MCP service for Cloud. Enterprise operators may instead package the stdio binary inside their controlled deployment. Then add and verify it under **MCP Servers**.
3. Create the supervisor, HR, and IT agents and attach only the tools each role needs.
4. Create a schema with the supervisor as its entry agent. Add directed relationships from the supervisor to the two specialists.
5. Enable **Accept chat requests** and use the bottom **Test Flow** panel to verify that HR and IT requests reach the intended specialist.
6. Connect a product through the schema chat endpoint or generate a widget for the schema.

The bundled employee and ticket records are fictional. Add authentication, authorization, redaction, and audit controls before adapting these tools to real company data.

## Current references

- [Schemas and delegation](https://syntheticbrew.ai/docs/admin/schemas/)
- [Agents](https://syntheticbrew.ai/docs/admin/agents/)
- [MCP servers](https://syntheticbrew.ai/docs/admin/mcp-servers/)
- [Widget embedding](https://syntheticbrew.ai/docs/admin/widgets/)

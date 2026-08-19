# HR Assistant Example

This example contains a Go MCP server with mock employee and leave-management tools plus sample handbook documents. Use those assets as patterns with SyntheticBrew Cloud or Enterprise.

The bundled Compose stack and YAML configuration target an older SyntheticBrew distribution and are not a current installation or import guide.

## Build the current workflow

1. Follow the [Cloud quick start](https://syntheticbrew.ai/docs/getting-started/quick-start/) or deploy [Enterprise](https://syntheticbrew.ai/docs/deployment/enterprise-on-prem/) in your infrastructure.
2. Create an embedding model and a Knowledge base. Upload the Markdown files under `config/knowledge/`, wait for each file to become **ready**, link the base to the HR agent, and enable its Knowledge capability.
3. Adapt `mcp-server/` into a remote Streamable HTTP MCP service for Cloud. Enterprise operators may instead package the stdio binary inside their controlled deployment. Add the server under **MCP Servers**, verify the catalog, and attach the employee and leave tools to the HR agent.
4. Put the HR agent in a chat-enabled schema and test policy lookup, balance lookup, and a leave request in the bottom **Test Flow** panel.
5. Use a structured interruption when a user must supply missing information. A background task cannot wait for user input.

The sample data is fictional. Add authorization checks, data minimization, audit requirements, and human escalation appropriate to your organization before connecting real employee data.

## Current references

- [Knowledge](https://syntheticbrew.ai/docs/admin/knowledge/)
- [MCP servers](https://syntheticbrew.ai/docs/admin/mcp-servers/)
- [Agents](https://syntheticbrew.ai/docs/admin/agents/)
- [Tasks and human input](https://syntheticbrew.ai/docs/admin/tasks/)

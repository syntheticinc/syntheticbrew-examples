# Company Assistant Example

This example contains a Go MCP server with mock employee and IT-support tools plus prompts for a supervisor, an HR specialist, and an IT specialist. Use the source as a pattern with SyntheticBrew Cloud or Enterprise.

The bundled Compose stack and YAML configuration target an older SyntheticBrew distribution and are not a current installation or import guide. Current delegation is configured with schema relationships rather than an agent-owned `can_spawn` field.

## What the example demonstrates

```text
Employee request
      |
      v
  supervisor
   /      \
  v        v
HR agent  IT support
  |          |
  +---- company-data MCP ----+
```

The supervisor decides whether a request belongs to HR or IT. In a current SyntheticBrew workflow, the schema contains `supervisor -> hr-agent` and `supervisor -> it-support` relationships. Each specialist receives only the tools required for its role.

Try requests such as:

- “How much vacation does Alice have left?” — the HR specialist looks up the employee and leave balance.
- “My VPN will not connect.” — the IT specialist searches the mock knowledge base.
- “I need a monitor for my home office.” — the IT specialist can create a mock support ticket.

## Reusable MCP tools

| Tool | Purpose |
| --- | --- |
| `get_employees` | List the fictional employee records. |
| `get_employee_by_id` | Read one employee record. |
| `get_leave_balance` | Read mock leave balances. |
| `create_ticket` | Create a mock IT ticket. |
| `search_knowledge_base` | Search the sample HR and IT articles. |

The server implements MCP over stdio. An Enterprise operator can package it alongside the runtime. For Cloud, keep the same schemas and handlers but expose them through a protected remote Streamable HTTP MCP service.

## Build the current workflow

1. Follow the [Cloud quick start](https://syntheticbrew.ai/docs/getting-started/quick-start/) or deploy [Enterprise](https://syntheticbrew.ai/docs/deployment/enterprise-on-prem/) in your infrastructure.
2. Adapt `mcp-server/` into a remote Streamable HTTP MCP service for Cloud. Enterprise operators may instead package the stdio binary inside their controlled deployment. Then add and verify it under **MCP Servers**.
3. Create the supervisor, HR, and IT agents and attach only the tools each role needs.
4. Create a schema with the supervisor as its entry agent. Add directed relationships from the supervisor to the two specialists.
5. Enable **Accept chat requests** and use the bottom **Test Flow** panel to verify that HR and IT requests reach the intended specialist.
6. Connect a product through the schema chat endpoint or generate a widget for the schema.

## Project map

```text
company-assistant/
├── mcp-server/
│   ├── main.go        # MCP protocol, tool schemas, and handlers
│   └── data.go        # fictional employees, leave, tickets, and articles
├── config/agents.yaml # historical prompts and tool intent; do not import as-is
├── scripts/           # historical seed helper
└── docker-compose.yml # historical standalone stack
```

To adapt it, replace the mock records, add authorization inside every tool handler, choose which specialist receives each tool, and rewrite the prompts for your policies. Do not give the supervisor every specialist action merely because the tools share one server.

## Troubleshooting

- **No delegation tool:** verify both schema relationships and start a new session.
- **Server works locally but not in Cloud:** stdio is local-process transport; deploy a remote HTTP transport reachable from Cloud.
- **A specialist sees the wrong tools:** split the MCP services or tool assignments so each agent has least privilege.
- **The response exposes another employee's data:** add caller identity and authorization checks before using any real source.

The bundled employee and ticket records are fictional. Add authentication, authorization, redaction, and audit controls before adapting these tools to real company data.

## Current references

- [Schemas and delegation](https://syntheticbrew.ai/docs/admin/schemas/)
- [Agents](https://syntheticbrew.ai/docs/admin/agents/)
- [MCP servers](https://syntheticbrew.ai/docs/admin/mcp-servers/)
- [Widget embedding](https://syntheticbrew.ai/docs/admin/widgets/)

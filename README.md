# SyntheticBrew Examples

This repository contains public example source for MCP tool servers, sample data, and product integrations. Use the examples as implementation patterns with [SyntheticBrew Cloud](https://syntheticbrew.ai/docs/getting-started/quick-start/) or [SyntheticBrew Enterprise](https://syntheticbrew.ai/docs/deployment/enterprise-on-prem/).

The bundled Docker Compose files and declarative configuration predate the current platform workflow. Reuse the MCP servers, prompts, and sample data, but follow the current documentation for platform setup. The old image references, local-admin credentials, session endpoints, and `can_spawn` fields are not current setup instructions.

## Examples

| Example | Reusable parts | Current platform workflow |
|---|---|---|
| [HR assistant](./hr-assistant/) | HR data MCP server and sample knowledge documents | Upload documents, link Knowledge, and connect the MCP tools to an agent. |
| [Support agent](./support-agent/) | Support data MCP server and router/specialist prompts | Create explicit schema relationships from the router to each specialist. |
| [Sales agent](./sales-agent/) | Product and quote MCP tools | Use structured interruptions for approvals in browser and REST clients. |
| [Company assistant](./company-assistant/) | Employee and IT-support MCP tools | Create a supervisor and specialists, then define their schema relationships. |
| [Widget integration](./widget-integration/) | Minimal widget host page | Generate a current schema-scoped embed snippet before adding appearance options. |

For a current, forkable end-to-end workflow, use the [support-agent template](https://github.com/syntheticinc/support-agent-example) with the [coding-agent onboarding guide](https://syntheticbrew.ai/docs/integration/connect-coding-agent/).

## Use an example safely

1. Start with the Cloud quick start or your supported Enterprise deployment.
2. Read the example README to understand its agent roles, tools, and sample data.
3. Adapt the Go MCP server to a transport reachable from your deployment.
4. Create current agents and a schema in Admin or with a coding agent; do not import the historical YAML unchanged.
5. Assign only the tools each role needs, then test through the schema's **Test Flow** panel.
6. Replace every mock authorization and business rule before connecting real data or actions.

The MCP servers are small Go programs and can be inspected without running an old platform stack. Their records are fictional and their in-memory mutations are not durable production storage.

## Common troubleshooting

- Cloud cannot launch a repository's local stdio binary; expose a protected remote MCP transport.
- Delegation comes from schema relationships. A checked-in `can_spawn` field is historical and is ignored by current declarative workflows.
- Current chat integrations use `/api/v1/schemas/{schema_name}/chat` and SSE, not the old create-session/message endpoints shown in repository history.
- A successful mock action does not demonstrate production authorization, idempotency, privacy, retention, or audit controls.

## Product options

- **SyntheticBrew Cloud** is the managed service operated by SyntheticBrew.
- **SyntheticBrew Enterprise** runs in customer-managed on-premises or private infrastructure with customer-controlled networking, identity, data, observability, backups, and upgrades.

## License

The example source in this repository is licensed under the MIT License. That license applies to these examples, not to the SyntheticBrew platform.

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

## Product options

- **SyntheticBrew Cloud** is the managed service operated by SyntheticBrew.
- **SyntheticBrew Enterprise** runs in customer-managed on-premises or private infrastructure with customer-controlled networking, identity, data, observability, backups, and upgrades.

## License

The example source in this repository is licensed under the MIT License. That license applies to these examples, not to the SyntheticBrew platform.

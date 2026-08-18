# SyntheticBrew Examples

This repository contains public example source for MCP tool servers, sample data, and product integrations. Use the examples as implementation patterns with [SyntheticBrew Cloud](https://syntheticbrew.ai/docs/getting-started/quick-start/) or a licensed [SyntheticBrew Enterprise](https://syntheticbrew.ai/docs/deployment/enterprise-on-prem/) deployment.

The bundled Docker Compose files and declarative configuration predate the current Cloud and Enterprise product model. They are retained as historical source examples, not as a supported SyntheticBrew installation path. Do not use the old SyntheticBrew image references, local-admin credentials, session endpoints, or `can_spawn` fields as current setup instructions.

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
- **SyntheticBrew Enterprise** is proprietary software deployed on customer-managed on-premises or private infrastructure using licensed artifacts supplied to entitled customers.

## License

The example source in this repository is licensed under the MIT License. That license applies to these examples, not to the SyntheticBrew platform.

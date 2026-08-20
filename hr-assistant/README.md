# HR Assistant Example

This example contains a Go MCP server with mock employee and leave-management tools plus sample handbook documents. Use those assets as patterns with SyntheticBrew Cloud or Enterprise.

The bundled Compose stack and YAML configuration target an older SyntheticBrew distribution and are not a current installation or import guide.

## What the example demonstrates

The HR assistant combines two different data surfaces:

- **Knowledge** for handbook prose such as PTO, benefits, onboarding, remote work, and conduct policies;
- an **MCP server** for exact employee records, leave balances, and a mock leave-request action.

This separation keeps frequently edited narrative policy in documents while live personal records remain behind authenticated tools.

| MCP tool | Purpose |
| --- | --- |
| `get_employee` | Find a fictional employee by ID, email, or name. |
| `get_leave_balance` | Read vacation, sick, and personal-day balances. |
| `submit_leave_request` | Validate and create a mock leave request. |

The five sample documents under `config/knowledge/` cover PTO, benefits, onboarding, remote work, and the code of conduct.

## Example conversations

- “How many vacation days do employees receive?” should search the uploaded PTO policy and cite the relevant source.
- “What is Alice Johnson's balance?” should identify the employee and call the balance tool rather than infer from a document.
- “Request vacation for next week” should collect the missing dates, type, and reason before calling the action.
- A sensitive or unsupported workplace issue should state the limitation and direct the employee to the approved human channel.

For a current product or REST integration, collect required fields with `show_structured_output` and resume the persisted interrupt. The historical `ask_user` and escalation configuration in `agents.yaml` is not a supported import recipe.

## Build the current workflow

1. Follow the [Cloud quick start](https://syntheticbrew.ai/docs/getting-started/quick-start/) or deploy [Enterprise](https://syntheticbrew.ai/docs/deployment/enterprise-on-prem/) in your infrastructure.
2. Create an embedding model and a Knowledge base. Upload the Markdown files under `config/knowledge/`, wait for each file to become **ready**, link the base to the HR agent, and enable its Knowledge capability.
3. Adapt `mcp-server/` into a remote Streamable HTTP MCP service for Cloud. Enterprise operators may instead package the stdio binary inside their controlled deployment. Add the server under **MCP Servers**, verify the catalog, and attach the employee and leave tools to the HR agent.
4. Put the HR agent in a chat-enabled schema and test policy lookup, balance lookup, and a leave request in the bottom **Test Flow** panel.
5. Use a structured interruption when a user must supply missing information. A background task cannot wait for user input.

## Project map

```text
hr-assistant/
├── config/knowledge/  # five fictional handbook documents
├── mcp-server/        # Go MCP server and fictional HR records
├── service/           # historical proxy/escalation example
├── config/agents.yaml # historical workflow intent; do not import as-is
└── docker-compose.yml # historical standalone stack
```

To customize the example, replace the documents through the Knowledge upload workflow, replace mock handlers with an authenticated HR API, and encode leave policy in the system of record rather than trusting the prompt to enforce it. Test missing identity, insufficient balance, invalid dates, and an unauthorized employee lookup.

## Troubleshooting

- **Knowledge returns nothing:** confirm the embedding model, wait for every document to become **ready**, link the base, and enable the Knowledge capability.
- **Old and new policy conflict:** delete the old file entry before uploading its replacement; duplicate filenames create separate entries.
- **The form never appears:** the client must render `interrupt_request` and resume the same session and interrupt ID.
- **The MCP action fails:** inspect Tool Call Log, then validate identity, tool arguments, transport, and upstream business rules.

The sample data is fictional. Add authorization checks, data minimization, audit requirements, and human escalation appropriate to your organization before connecting real employee data.

## Current references

- [Knowledge](https://syntheticbrew.ai/docs/admin/knowledge/)
- [MCP servers](https://syntheticbrew.ai/docs/admin/mcp-servers/)
- [Agents](https://syntheticbrew.ai/docs/admin/agents/)
- [Tasks and human input](https://syntheticbrew.ai/docs/admin/tasks/)

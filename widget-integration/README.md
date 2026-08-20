# Widget Integration Example

This directory contains a minimal HTML host page for the SyntheticBrew chat widget. Its checked-in placeholder markup predates the current schema-based embed flow; generate a fresh snippet before using the page.

## Create a current embed

1. Enable **Accept chat requests** on the intended schema.
2. Use the `get_embed_snippet` management MCP tool with the schema name. It returns a complete script tag and a newly issued chat-scoped key.
3. Copy the appearance attributes you want from **Admin → Widgets** onto that generated snippet.
4. Replace the placeholder script in `index.html`, open the page, and send a test message.

The Admin Widgets page intentionally generates appearance settings without a credential. A working direct embed needs the chat-scoped key returned by `get_embed_snippet`. Anyone who can view the page can read that key, so keep it limited to Chat scope, restrict allowed widget origins, monitor its use, and revoke it when the page is retired.

## Supported attributes

| Attribute | Required | Purpose |
| --- | --- | --- |
| `data-schema` | Yes | Chat-enabled schema name. |
| `data-api-key` | Direct mode | Chat-scoped key included by `get_embed_snippet`. |
| `data-endpoint` | Proxy mode | Base URL of a compatible proxy; the widget appends `/api/v1/schemas/{name}/chat`. |
| `data-position` | No | `bottom-right` or `bottom-left`. |
| `data-theme` | No | `light` or `dark`. |
| `data-primary-color` | No | Widget accent color. |
| `data-title` | No | Panel title. |
| `data-welcome` | No | Initial message. |
| `data-placeholder` | No | Composer placeholder. |

In direct mode the widget loads `widget.js` and calls SyntheticBrew with `data-api-key`. In proxy mode, `data-endpoint` points at a backend that exposes the same schema-chat path and SSE contract; that backend can add application authentication, user identity, and rate controls before calling SyntheticBrew. Do not combine an unrestricted administrative key with either mode.

## Troubleshooting

- **The bubble appears but chat returns 401:** generate a complete snippet; the Admin appearance preview contains no credential.
- **Chat returns 404:** confirm `data-schema` uses the schema name and **Accept chat requests** is enabled.
- **The script is not found:** use the visitor-reachable SyntheticBrew origin, including the correct path through your Enterprise ingress.
- **Styling does not change:** use the exact attribute names above and remove duplicate widget script tags.

See the current [widget embedding guide](https://syntheticbrew.ai/docs/admin/widgets/) for the supported attributes and troubleshooting steps.

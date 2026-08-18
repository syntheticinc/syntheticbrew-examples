# Widget Integration Example

This directory contains a minimal HTML host page for the SyntheticBrew chat widget. Its checked-in placeholder markup predates the current schema-based embed flow; generate a fresh snippet before using the page.

## Create a current embed

1. Enable **Accept chat requests** on the intended schema.
2. Use the `get_embed_snippet` management MCP tool with the schema name. It returns a complete script tag and a newly issued chat-scoped key.
3. Copy the appearance attributes you want from **Admin → Widgets** onto that generated snippet.
4. Replace the placeholder script in `index.html`, open the page, and send a test message.

The Admin Widgets page intentionally generates appearance settings without a credential. A working direct embed needs the chat-scoped key returned by `get_embed_snippet`. Anyone who can view the page can read that key, so keep it limited to Chat scope, restrict allowed widget origins, monitor its use, and revoke it when the page is retired.

See the current [widget embedding guide](https://syntheticbrew.ai/docs/admin/widgets/) for the supported attributes and troubleshooting steps.

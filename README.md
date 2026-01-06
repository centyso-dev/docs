# Chucky SDK Documentation

Documentation for the Chucky SDK - Claude as a Service.

## Structure

```
docs/
├── index.mdx              # Introduction
├── quickstart.mdx         # Getting started guide
├── authentication.mdx     # Token and budget management
├── concepts/
│   ├── sessions.mdx       # Multi-turn conversations
│   ├── tools.mdx          # Custom tools
│   ├── mcp-servers.mdx    # MCP server bundles
│   └── streaming.mdx      # Streaming responses
├── advanced/
│   ├── error-handling.mdx # Error handling
│   ├── budget-management.mdx # Budget strategies
│   └── workspace.mdx      # Workspace configuration
└── sdk/
    ├── javascript/        # JS/TS SDK reference
    │   ├── client.mdx
    │   ├── session.mdx
    │   ├── tools.mdx
    │   └── types.mdx
    └── python/            # Python SDK reference
        ├── client.mdx
        ├── tools.mdx
        └── types.mdx
```

## Development

Install the [Mintlify CLI](https://www.npmjs.com/package/mint) to preview locally:

```bash
npm i -g mint
```

Run the dev server:

```bash
mint dev
```

View at `http://localhost:3000`.

## Publishing

Changes pushed to the default branch are automatically deployed.

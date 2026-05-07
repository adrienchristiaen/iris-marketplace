# iris-marketplace

Curated catalog of skills, MCP servers, and themes for the [Iris CLI](https://github.com/adrienchristiaen/JARVIS).

`/marketplace` inside Iris fetches `catalog.json` from this repo at runtime
and lets users install items directly from there.

## Schema

```json
{
  "version": 1,
  "updated_at": "YYYY-MM-DD",
  "items": [
    {
      "slug": "unique-id",
      "name": "Human Name",
      "kind": "skill | mcp | theme | hook",
      "description": "One-line description shown in the marketplace UI.",
      "author": "github-handle-or-org",
      "version": "0.1",
      "install_kind": "claude_plugin | builtin | mcp_npx | builtin_theme | git_clone",
      "install_url": "kind-specific install target",
      "tags": ["search", "keywords"]
    }
  ]
}
```

### `install_kind` semantics

| kind             | `install_url` example                            | Iris action                                                       |
|------------------|--------------------------------------------------|--------------------------------------------------------------------|
| `claude_plugin`  | `JuliusBrussee/caveman`                          | `claude plugin marketplace add` + `install`                       |
| `builtin`        | `frontend-design@claude-plugins-official`        | `claude plugin install <url>`                                     |
| `mcp_npx`        | `@modelcontextprotocol/server-filesystem`        | append `[[mcp.servers]]` entry to iris config (npx -y <pkg>)      |
| `builtin_theme`  | `gruvbox`                                        | register palette in `iris.ui.theme.PALETTES` (bundled defs)       |
| `git_clone`      | `https://github.com/foo/bar.git`                 | `git clone` to `~/.iris/skills/<slug>/`                           |

## Contributing

Open a PR adding an entry to `catalog.json`. Keep the description ≤ 110 chars
and tags lower-case.

Items must be:
- Free / open-source
- Installable via one of the supported `install_kind`s
- Curated for quality (not auto-imported lists)

## License

MIT.

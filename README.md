# innernet-mcp tooling

release tooling for the innernet plugin, kept off `main` so the plugin folder holds
only what the claude directory accepts (markdown, text, json, yaml, images).

- `check.py` — the package contract. ci runs it on every push to `main`:
  `python3 .tools/check.py --root=.` (pass `--offline` to skip the live tool list).
- `publish-registry.sh` — publishes `server.json` to the official MCP registry.
  run it from a `main` checkout: `bash path/to/publish-registry.sh .`

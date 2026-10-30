# FilmLab for Claude Code

Includes the remote FilmLab MCP server and two skills: `filmlab-film` takes a brief to a finished, editable film;
`filmlab-schnittplatz` guides timeline handover to Resolve, Premiere or Final Cut.

From the repository root, load it for one session:

```sh
claude --plugin-dir integrations/claude-plugin/filmlab
```

Or install through the local marketplace:

```sh
claude plugin marketplace add integrations/claude-plugin
claude plugin install filmlab@thefilmradar
```

Sign in via `/mcp` → `plugin:filmlab:filmlab` → Authenticate. Claude Code uses
the server's OAuth discovery; no token configuration is needed. If you already
added `filmlab` with `claude mcp add` using the same URL, Claude Code recognizes
that URL and does not create a second server.

The local FilmLab bridge (DaVinci Resolve control, local export) is not part of
this plugin. It also serves every FilmLab tool under its own key, so with both
loaded each FilmLab tool would appear twice. If you need Resolve control, add
the bridge from the FilmLab installer separately, as described in the FilmLab
handbook.

The skills are generated. Edit `shared/agenten-weg.ts`, then run:

```sh
node --experimental-strip-types scripts/agenten-skill/erzeuge.mjs
```

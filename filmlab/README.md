# FilmLab for Claude Code

Includes the remote FilmLab MCP server and two skills: `filmlab-film` takes a brief to a finished, editable film;
`filmlab-schnittplatz` guides timeline handover to Resolve, Premiere or Final Cut.

Install from the FilmRadar marketplace:

```sh
claude plugin marketplace add thefilmradar/claude-plugins
claude plugin install filmlab@thefilmradar
```

Or load it for one session from a checkout of the marketplace (the folder that
holds `.claude-plugin/marketplace.json`):

```sh
claude --plugin-dir ./filmlab
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

The skills are generated from FilmRadar's main repository; edits made here are
overwritten by the next release.

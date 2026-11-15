# Google Stitch connection

Requested project: **Roofscapes Research Studio**. Persistent design context is
stored in [design-tools.json](../design-tools.json). Its `project_url` and
`project_resource` remain null until the real Stitch service returns them.

The official endpoint `https://stitch.googleapis.com/mcp` is registered as the
global Codex MCP server `stitch`. Automatic OAuth registration returned
`Dynamic client registration not supported`. The connector therefore uses Stitch's
documented API-key authentication through a local Windows credential helper.
Registration is complete; authentication is pending until the user enters a key.

Use the masked setup window already opened, or launch it locally:

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File ui/integrations/setup-stitch.ps1
```

Sign in at [Stitch](https://stitch.google.com/?pli=1), create an API key in
Settings → API Keys, and paste it into that local masked prompt. Do not paste it
into chat. The credential is encrypted using Windows DPAPI for the current user
under local AppData (`Roofscapes/Stitch/credential.xml`), outside this repository.
The helper decrypts it only for request headers; it is not written to source,
browser JavaScript, exports, reports or Git. Never run the header helper directly
in a logged/shared terminal: its output is for Codex's internal header channel.

Setup verifies the MCP handshake/tool catalog and creates the explicitly requested
project if the service's creation schema is compatible. A prior uncertain creation
attempt must be reviewed using `list_projects` before retrying; the script avoids
blind duplicate creation. The configuration records only service-returned project
identifiers/URLs. No guessed project link is treated as an existing project.

After successful setup, restart the Codex extension to load the new connector.
Verify registration with `codex mcp get stitch --json`; the header helper is redacted.
Account verification can be repeated without creating a project:

```powershell
.\.venv\Scripts\python.exe -m ui.integrations.stitch
```

Future Codex sessions: read `ui/design-tools.json` and this file. Once authenticated,
use the returned project resource for graphic changes, preserve the seven views
and data bindings, and review changes against `ui/docs/screenshots/`. Screenshot
references, the original prototype and [the project brief](../stitch/PROJECT_BRIEF.md)
are ready. No UI assets have been uploaded and no Stitch design was generated
before authentication. Scientific source files remain the authority for numbers.

Official references: [Google Stitch MCP setup](https://stitch.google.com/docs/mcp/setup/),
[Google-hosted readable setup](https://app-companion-430619.appspot.com/docs/mcp/setup/index.html),
[Codex MCP configuration](https://learn.chatgpt.com/docs/extend/mcp?surface=cli).

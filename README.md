# /call-me for Omarchy

One-time setup panel for connecting the [/call-me](https://github.com/radres/call-me)
phone app (iPhone or Android) to your AI agents. Your agent rings your actual phone, speaks its
question, and gets your spoken answer back as text.

This repository holds only the Omarchy plugin: the Quickshell panel, a launcher
entry script, and the icon. The Claude Code plugin, Codex MCP server, and agent
skill live in [radres/call-me](https://github.com/radres/call-me).

## What it does

- Reads your paired callme number from `~/.aiphone/config.json`.
- Shows copy-ready setup instructions for Claude Code, Codex, Gemini CLI,
  OpenCode, and plain HTTP.
- **Test calls** sends a real text or call to your phone through
  `https://serdaroztetik.com/aiphone` so you can verify delivery.
- Never writes to `~/.aiphone/config.json` without an explicit pairing action.
- No persistent bar icon. Day-to-day use happens through the AI/MCP tools.

## Requirements

- Omarchy with `omarchy-shell` (Quickshell panels).
- /call-me from the [App Store](https://callmemcp.com/go/readme) or
  [Google Play](https://callmemcp.com/go/play-omarchy), paired once on the phone. No account, no email.
- `curl` and `jq` on the machine. The panel shells out to both.

## Install

```bash
omarchy plugin add https://github.com/radres/omarchy-plugin-call-me.git --enable
```

Register the Super+Space launcher entry:

```bash
bash ~/.config/omarchy/plugins/radres.call-me/install-launcher.sh
```

This copies the icon to `$XDG_DATA_HOME/icons` and writes one `.desktop` file
under `$XDG_DATA_HOME/applications` (default `~/.local/share`). No sudo, no
downloads, no package installs.

Search `/call-me`, `callme`, or `phone` with Super+Space to open setup.

## Remove

```bash
omarchy plugin remove radres.call-me
rm -f ~/.local/share/applications/radres.call-me.desktop \
      ~/.local/share/icons/hicolor/512x512/apps/radres.call-me.png
```

## Network and data

The panel makes network requests only when you press **Text me** or **Call me**
under Test calls, or when you pair a number. Requests go to
`https://serdaroztetik.com/aiphone`. Your 10-digit number is a bearer
credential: anyone who knows it can reach you. Keep it out of shared prompts
and logs.

## License

MIT. See [LICENSE](LICENSE).

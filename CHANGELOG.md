# Cambios

## 0.2.0

- El MCP de Weppa (`https://mcp.weppa.co/mcp`) se conecta por OAuth: el plugin ya no lleva el encabezado
  `Authorization` ni lee una variable de entorno con un token. Si tenías configurado `weppa` con una
  clave, quítalo y vuelve a instalar el plugin.
- Instalación como la de Cloudflare: plugin para Claude Code, y `npx skills` + MCP para los demás.
- `.claude-plugin/plugin.json` lleva el digest de la skill, el mismo con que el MCP sirve
  `skill://use-weppa/SKILL.md`.

## 0.1.0

- Primera versión pública de la skill `use-weppa`.
- Plugin para Claude Code, Codex y Cursor con el MCP de Weppa (`https://mcp.weppa.co/mcp`).
- El token se leía de una variable de entorno.
- Lista pública de los flujos certificados en `evals/scenarios.md`.

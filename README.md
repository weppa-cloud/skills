# Skills de Weppa

Skill y plugin para que tu agente (Claude Code, Codex, Cursor u otro compatible con
[Agent Skills](https://agentskills.io)) opere las apps de tu cuenta de [Weppa](https://weppa.co)
por el MCP de Weppa (`https://mcp.weppa.co/mcp`).

Con la skill `use-weppa`, tu agente puede:

- decirte cómo están tus apps, leer sus logs y diagnosticar por qué una no carga;
- reiniciar, pausar, reanudar y bajar de tamaño una app;
- pedir una copia protegida y darte un enlace para descargar tus datos;
- conectar tu dominio y publicar tu Weppa Site;
- preparar lo que tú confirmas en el visor: crear, borrar, restaurar, duplicar o subir de tamaño.

Tu agente nunca ve el valor de tus claves y nunca toca otra cuenta. Lo que destruye datos o genera
un cobro lo confirmas tú en el visor.

## Lo más fácil: que lo instale tu agente

Copia esto en tu agente:

> Conéctame a Weppa siguiendo las instrucciones de https://visor.weppa.co/agent-setup/prompt.md.
> Haz la configuración que puedas y guíame únicamente en los pasos que necesiten mi intervención.

Tu agente instala la skill y el MCP con los comandos de abajo y te pide solo que inicies sesión en
Weppa y autorices.

## El MCP de Weppa: OAuth, sin claves

- Nombre: `weppa`
- Transporte: Streamable HTTP
- Dirección: `https://mcp.weppa.co/mcp`
- Autenticación: OAuth. Inicias sesión en tu navegador, eliges la cuenta y el permiso («Solo mirar»
  viene marcado) y pulsas «Autorizar». No hace falta ninguna clave.

No pegues contraseñas, claves ni códigos en el chat del agente: no hacen falta. Ves y revocas cada
acceso en https://visor.weppa.co/agent/tokens.

## Instalación

### Claude Code

El plugin instala la skill y el MCP de una vez:

```sh
claude plugin marketplace add weppa-cloud/skills
claude plugin install weppa@weppa
```

Después, en Claude Code, escribe `/reload-plugins` (o abre una sesión nueva), luego `/mcp`, elige
`plugin:weppa:weppa` e inicia sesión. No uses `npx skills` ni `claude mcp add` para Weppa: el plugin
ya trae las dos cosas.

### Codex, Cursor, OpenCode, VS Code y otros

Primero la skill:

```sh
(cd "$(mktemp -d)" && npx -y skills@1.7.4 add weppa-cloud/skills --skill '*' --yes --global)
```

Con la versión fija y desde una carpeta vacía, `npx` no usa un `skills` que traiga tu proyecto.

Después el MCP, en la configuración de tu agente. La sesión se inicia sola la primera vez que el
agente usa Weppa, o con el comando de inicio de sesión de tu herramienta.

**Codex:**

```sh
codex mcp add weppa --url https://mcp.weppa.co/mcp
codex mcp login weppa
```

**Cursor** (`~/.cursor/mcp.json`, dentro de `mcpServers`):

```json
"weppa": { "url": "https://mcp.weppa.co/mcp" }
```

**VS Code** (GitHub Copilot):

```sh
code --add-mcp '{"name":"weppa","type":"http","url":"https://mcp.weppa.co/mcp"}'
```

**OpenCode** (`~/.config/opencode/opencode.json`, dentro de `mcp`), y después `opencode mcp auth weppa`:

```json
"weppa": { "type": "remote", "url": "https://mcp.weppa.co/mcp", "enabled": true, "oauth": {} }
```

### Sin instalar nada

Si tu agente no permite instalar skills (por ejemplo, Claude en la web o ChatGPT), conecta solo el
MCP: el servidor sirve la misma skill en `skill://use-weppa/SKILL.md`, con los mismos bytes que este
repositorio.

## Actualizar

- **Claude Code:** `claude plugin marketplace update weppa` y `claude plugin update weppa@weppa`, o
  activa la actualización automática del marketplace en `/plugin` → Marketplaces.
- **`npx skills`:** vuelve a correr el comando de arriba, tal cual.

Cada versión del plugin dice qué skill trae: `.claude-plugin/plugin.json` lleva la versión
(`0.3.9`) y el digest de `skills/use-weppa/SKILL.md` (`sha256:650ab934a48efd6fc6d49131e86c0345249671154b153e772bbf044c2a7121c8`). Es el mismo digest
con que el MCP anuncia `skill://use-weppa/SKILL.md`: si coinciden, tienes la misma skill.

## Prueba rápida

Con el MCP conectado, pregúntale a tu agente:

- «¿Cómo están mis apps?»
- «Mi app no carga: revisa qué pasa.»
- «Haz una copia de mi app.»

Si responde que no tiene permiso (401), inicia sesión de nuevo en el MCP `weppa`. Si una acción se
niega (403) con «Solo mirar», autoriza de nuevo con «Operar».

## Contenido

| Ruta | Qué es |
|---|---|
| `skills/use-weppa/SKILL.md` | La skill |
| `.mcp.json` | El MCP de Weppa para el plugin (OAuth, sin claves) |
| `.claude-plugin/` | Plugin y marketplace de Claude Code |
| `.codex-plugin/`, `.agents/plugins/` | Plugin y marketplace de Codex |
| `.cursor-plugin/` | Plugin de Cursor |
| `evals/scenarios.md` | Los flujos que certificamos |

## Licencia

[Apache-2.0](LICENSE). Versión 0.3.9.

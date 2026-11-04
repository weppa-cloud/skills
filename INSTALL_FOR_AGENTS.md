# Instalación para agentes

Eres un agente de código. Tu usuario te pidió instalar las skills de Weppa. Las instrucciones
oficiales y completas, con una sección por herramienta, están en
https://visor.weppa.co/agent-setup/prompt.md: síguelas. Este archivo es su resumen.

Haz tú los pasos que tu herramienta te deje hacer. Pídele a la persona solo que inicie sesión en
Weppa y autorice.

## Reglas

- La conexión es OAuth: no hace falta ninguna clave. No pidas contraseñas, claves, tokens ni códigos
  en el chat, y no los uses si te los pegan: di que no hacen falta y que revoquen esa clave en
  https://visor.weppa.co/agent/tokens.
- Conserva los servidores MCP, skills e instrucciones que ya hay. Agrega solo `weppa`; si ya existe,
  actualízalo en vez de duplicarlo.
- Si ya hay un `weppa` con un encabezado `Authorization` (una clave vieja), quítalo entero antes, sin
  mostrar ni copiar su valor.
- No digas que quedó conectado hasta que la comprobación del final responda.

## Claude Code

El plugin instala la skill y el MCP de una vez. No uses `npx skills` ni `claude mcp add` para Weppa.

```sh
claude plugin marketplace add weppa-cloud/skills
claude plugin install weppa@weppa
```

Pídele a la persona que escriba `/reload-plugins` (o abra una sesión nueva), luego `/mcp`, elija
`plugin:weppa:weppa` e inicie sesión.

## Otros agentes

Instala la skill:

```sh
(cd "$(mktemp -d)" && npx -y skills@1.7.4 add weppa-cloud/skills --skill '*' --yes --global)
```

Córrelo tal cual: con la versión fija y desde una carpeta vacía, `npx` no usa un `skills` del proyecto.

Después registra el MCP en la configuración de usuario de tu agente: servidor `weppa`, Streamable
HTTP, `https://mcp.weppa.co/mcp`, autenticación OAuth, sin encabezados. Por ejemplo, en Codex:

```sh
codex mcp add weppa --url https://mcp.weppa.co/mcp
codex mcp login weppa
```

Si tu herramienta no permite instalar skills, conecta solo el MCP y lee la skill del propio servidor:
`skill://use-weppa/SKILL.md` (`resources/read`).

## Comprobar

Con la sesión iniciada, llama a `weppa_projects_list` (solo lectura) y di qué apps tiene la cuenta.
Si no aparecen tus herramientas de `weppa`, pide a la persona que abra una sesión nueva.

Dile al dueño: «Listo. Ya puedo operar tus apps de Weppa. Prueba con: ¿cómo están mis apps?».

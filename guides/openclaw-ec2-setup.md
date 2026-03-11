# 🚀 Instalar OpenClaw en AWS EC2 (Ubuntu)

Guía paso a paso para levantar tu propio agente OpenClaw en un VPS de Amazon EC2.

---

## 📋 Requisitos previos

- Una instancia **EC2** con **Ubuntu 22.04+**
- Tipo recomendado: `t3.small` o superior (2 GB RAM mínimo)
- **Security Group** con puerto **22** (SSH) abierto
- Tu **API key** de un proveedor de LLM (Anthropic, OpenAI, etc.)

---

## Paso 1 — Conectarte al VPS

```bash
ssh -i tu-key.pem ubuntu@TU_IP_PUBLICA
```

---

## Paso 2 — Actualizar el sistema

```bash
sudo apt update && sudo apt upgrade -y
```

---

## Paso 3 — Instalar Node.js 22

```bash
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
```

> ⚠️ **Si te da error de conflicto con `libnode-dev`**, corré esto primero:
>
> ```bash
> sudo apt remove -y libnode-dev nodejs-doc
> sudo apt autoremove -y
> ```

Después instalá Node:

```bash
sudo apt install -y nodejs
node --version  # Verificar que sea v22+
```

---

## Paso 4 — Instalar OpenClaw

```bash
curl -fsSL https://openclaw.ai/install.sh | bash
```

> 💡 Este script instala OpenClaw sin necesidad de `sudo`. Si preferís usar npm directamente:
>
> ```bash
> npm install -g openclaw
> ```
>
> **Nota:** No uses `sudo npm install -g` — puede causar errores de permisos con git.

---

## Paso 5 — Configurar OpenClaw (wizard)

```bash
openclaw onboard --install-daemon
```

El wizard te guía por:

1. **Modelo y API Key** — Elegí tu proveedor (Anthropic, OpenAI, etc.) y pegá tu API key
2. **Workspace** — Dónde se guardan los archivos del agente
3. **Gateway** — Puerto (default: 18789) y autenticación
4. **Canales** — Conectar Slack, Discord, Telegram, WhatsApp, etc.
5. **Daemon** — Instala el servicio systemd para que arranque automáticamente

---

## Paso 6 — Verificar que está corriendo

```bash
openclaw gateway status
```

---

## Paso 7 — Abrir el dashboard

```bash
openclaw dashboard
```

O desde tu browser: `http://TU_IP:18789/`

---

## 🔒 Tips de seguridad

- **No expongas el puerto 18789 directo a internet** — usá un reverse proxy (nginx/caddy) con HTTPS
- Si querés acceso remoto seguro, configurá **Tailscale** durante el wizard
- Mantené tu API key segura — nunca la compartas

---

## 🔧 Troubleshooting

| Problema | Solución |
|----------|----------|
| `Permission denied` en `apt` | Agregar `sudo` antes del comando |
| Conflicto con `libnode-dev` | `sudo apt remove -y libnode-dev nodejs-doc && sudo apt autoremove -y` |
| `EACCES` con `npm install -g` | Usar el install script en vez de `sudo npm` |
| Gateway no responde | `openclaw gateway restart` |

---

## 📖 Recursos

- **Documentación oficial:** [docs.openclaw.ai](https://docs.openclaw.ai)
- **GitHub:** [github.com/openclaw/openclaw](https://github.com/openclaw/openclaw)
- **Comunidad Discord:** [discord.com/invite/clawd](https://discord.com/invite/clawd)

---

*Guía creada por [Atenea Conocimientos](https://ateneaconocimientos.com) — última actualización: marzo 2026*

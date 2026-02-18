# 🤖 Guía de Instalación de OpenClaw

> **📅 Última actualización:** 18 de Febrero 2026  
> **⚠️ Estado:** Beta - Esta guía puede quedar desactualizada. Consultá siempre la [documentación oficial](https://docs.openclaw.ai).

---

## ⚠️ DISCLAIMER - LEER ANTES DE CONTINUAR

**OpenClaw es una herramienta poderosa que tiene acceso completo a tu terminal y sistema de archivos.**

- 🔴 **Instalá bajo tu propio riesgo**
- 🔴 **No lo instales en tu máquina principal de trabajo si no entendés las implicaciones**
- 🔴 **Recomendamos usar una VM o VPS para experimentar**
- 🔴 **Nunca expongas el agente a mensajes de desconocidos sin configurar restricciones**

**Atenea Conocimientos no se hace responsable por pérdida de datos, brechas de seguridad, o cualquier otro problema derivado del uso de esta herramienta.**

Si decidís continuar, hacelo con precaución y entendiendo los riesgos.

---

## ¿Qué es OpenClaw?

OpenClaw es un **gateway de mensajería auto-hospedado** que conecta plataformas como WhatsApp, Telegram, Discord con agentes de IA. Es un proceso que corre en tu máquina y permite que un LLM (como Claude) ejecute tareas reales: gestionar archivos, correr comandos, revisar emails, etc.

### ¿En qué se diferencia de ChatGPT/Claude web?

- Es **auto-hospedado** en tu máquina
- Puede **ejecutar comandos** en tu terminal
- Soporta **múltiples canales** de comunicación
- Es altamente **configurable y extensible**

---

## Requisitos Previos

- **Node.js v22+** (verificar con `node --version`)
- Familiaridad básica con terminal/CLI
- Una API key de un proveedor de LLM (Anthropic, OpenAI, o Google)

---

## 1. Instalación

```bash
# Instalar globalmente
npm install -g openclaw

# Verificar instalación
openclaw --version
```

---

## 2. Configuración Inicial

```bash
openclaw onboard --install-daemon
```

El asistente te guiará paso a paso:

1. **Tipo de gateway** → `Local gateway` (para tu máquina)
2. **Workspace** → Dejá el default `~/.openclaw`
3. **Modelo de IA** → Anthropic (Claude) recomendado
4. **API Key** → Tu clave del proveedor elegido
5. **Puerto** → Default `18789`
6. **Bind** → `Loopback` (más seguro, solo local)

---

## 3. Primer Contacto

```bash
openclaw tui
```

Se abre la interfaz de terminal. El agente te pedirá tu nombre y se presentará.

---

## 4. Archivos Importantes

| Archivo | Descripción |
|---------|-------------|
| `agent.md` | Instrucciones principales del agente |
| `identity.md` | Nombre y personalidad |
| `memory.md` | Recuerdos acumulados |
| `user.md` | Info sobre vos (nombre, timezone) |
| `tools.md` | Notas sobre herramientas |

Todos están en `~/.openclaw/`

---

## 5. Comandos Útiles

```bash
# Estado del gateway
openclaw status

# Health check
openclaw doctor

# Auditoría de seguridad
openclaw security audit deep

# Reiniciar gateway
openclaw gateway restart
```

Dentro de la TUI, escribí `/` para ver todos los comandos disponibles.

---

## 🔒 SEGURIDAD - MUY IMPORTANTE

### Riesgos Principales

1. **Prompt Injection** — Alguien puede enviar mensajes maliciosos que engañen al agente para ejecutar comandos dañinos
2. **Acceso Total** — El agente puede leer/escribir/borrar cualquier archivo de tu sistema
3. **Ejecución de Comandos** — Puede correr cualquier comando en tu terminal

### Mejores Prácticas

| Práctica | Por qué |
|----------|---------|
| Usá un modelo potente | Los modelos grandes son más resistentes a inyecciones |
| Ejecutá `openclaw security audit deep` | Detecta configuraciones inseguras |
| Configurá `allow_from` en canales | Solo acepta mensajes de números/usuarios específicos |
| **NUNCA** lo pongas en un grupo público | Solo conversaciones 1:1 |
| Considerá usar un VPS | Aislá el agente de tus archivos importantes |
| Usá sandboxing (Docker) | Aísla al agente en un contenedor |

### Bloquear Herramientas Peligrosas

Podés configurar `tool.deny` para bloquear herramientas como `exec`, `process`, `browser` en agentes expuestos a input no confiable.

---

## 6. Conectar WhatsApp (Opcional)

```bash
# Habilitar plugin
openclaw plugins enable whatsapp

# Reiniciar
openclaw gateway restart

# Login (escanear QR)
openclaw channels login
```

**⚠️ Recomendación:** Usá un número de teléfono dedicado, no tu número personal.

---

## 7. Conectar Discord (Opcional)

1. Crear app en [Discord Developer Portal](https://discord.com/developers/applications)
2. Crear bot y copiar token
3. Habilitar "Message Content Intent"
4. Invitar bot a un servidor **privado**
5. Configurar en OpenClaw con el token, guild ID y channel ID

**⚠️ NUNCA** pongas el bot en un servidor público.

---

## 8. Multi-Agente

```bash
# Crear nuevo agente
openclaw agents add work

# Listar agentes
openclaw agents list

# Cambiar en TUI
/agents
```

Útil para separar agente personal de agente de trabajo.

---

## Recursos

- 📚 [Documentación Oficial](https://docs.openclaw.ai)
- 💻 [GitHub](https://github.com/openclaw/openclaw)
- 🔌 [ClawHub - Skills](https://clawhub.com)
- 💬 [Discord Community](https://discord.com/invite/clawd)

---

## ¿Problemas?

1. Corré `openclaw doctor` para diagnóstico
2. Revisá los logs en `~/.openclaw/logs/`
3. Preguntá en el Discord de OpenClaw

---

*Guía creada por Atenea Conocimientos para la comunidad de QA.*  
*Basada en la documentación oficial y el curso de freeCodeCamp.*

**Recordá: Usá esta herramienta de manera responsable y bajo tu propio riesgo.** 🦉

# Claude 

Claude es un modelo de inteligencia artificial creado por la empresa Anthropic, diseñado para entender, razonar y generar texto de forma segura y útil.

Usi eb escenario común:

* claude.ai (suscripción): Para desarrollo, prototipado, debugging, exploración de ideas, recomendado para usarlo durante el desarrollo para promps, estrategias, generar código, debugging y refinamiento 
* API (por consumo): Para la aplicación en producción que tus usuarios finales utilizan por ejemplo en integrar a la aplicación, servir a usuarios finales, escalar segùn demanda


## Instalar Claude Code en la terminal (CLI)

1. Instalar Node.js

Verifica si esta instalado Node.js 18+

```sh
node --version
```

Si no esta instalar Instalar Node.js

2. Instalar Claude Code CLI

```sh
# Instalar globalmente via npm
npm install -g @anthropic-ai/claude-code

# Verificar instalación
claude --version
```

3. Autenticar

```sh
# Primera vez - configurar API key
claude auth

# Seguir las instrucciones del navegador
claude auth
```

4. Usar desde Terminal de VS Code

```sh
# Abre el terminal integrado de VS Code
# Ctrl+J o View > Terminal

# Navega a tu proyecto
cd /ruta/proyecto

# Inicia Claude Code
claude

# O modo directo sin interactivo
claude -p "analiza este código y encuentra bugs"
```


## Instalación Extensión VS Code

1. Instalar la Extensión

```sh
# Buscar en marketplace el paquetes: "Claude Code"
# Click: Install
```

2. Autenticación

Al abrir la extensión por primera vez:

    Click en el ícono ✱ Spark (esquina superior derecha del editor)
    Te pedirá iniciar sesión con tu cuenta Anthropic
    Sigue el proceso OAuth

Requisitos:

Cuenta Anthropic (Pro o Max para uso completo)
VS Code actualizado

3. Usar Claude Code

Formas de abrir:

```sh
# 1. Click en ícono Spark ✱ (top-right del editor)
# 2. Command Palette: Cmd+Shift+P (Mac) / Ctrl+Shift+P (Windows), luego escribir: "Claude Code: Open in New Tab"
# 3. Status Bar: Click en "✱ Claude Code" (abajo a la derecha)

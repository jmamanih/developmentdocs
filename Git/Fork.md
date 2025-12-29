# Gestor gráfico de Git

Fork es un cliente gráfico de Git para macOS y Windows. Su objetivo es facilitar el uso de Git mediante una interfaz visual clara y poderosa, sin tener que usar la línea de comandos todo el tiempo.

Es básicamente una forma más visual de hacer todo esto (y más):

* Ver ramas y commits con un historial gráfico interactivo.
* Hacer merge, rebase, stash, cherry-pick.
* Resolver conflictos de manera visual.
* Ver diferencias entre archivos (diff) antes y después de commits.
* Administrar múltiples repositorios fácilmente.
* Integración con GitHub, GitLab, Bitbucket, etc.

## Instalación

📥 Sitio oficial

Se puede descargar de:

    👉 https://fork.dev

## Habilitar fork en la línea de comandos

Abrir Fork.

En la barra de menú:

    Fork > Settings > Integrations

Verás una opción para instalar la herramienta de línea de comandos.

    Haz clic en “Install Command Line Tool”.

Esto instalará un comando llamado fork accesible desde tu terminal.

✅ Uso básico del comando fork

Para abrir el repositorio actual en Fork:

```sh
fork .
```

Para abrir un repositorio específico:

```sh
fork /ruta/a/tu/repositorio
```

💡 Tip adicional
Se puede crear un alias personalizado si asi lo prefieres:

```sh
alias forkapp="open -a Fork"
```
Y luego usarlo así:

```sh
forkapp .
```
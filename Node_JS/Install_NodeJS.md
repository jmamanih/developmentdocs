# Instalar Node JS en MacOs

## **Verificar la versión actual de Node.js**
Para verificar la versión instalada de Node.js y npm en tu macOS:

Abrir la terminal.

Escribir el siguiente comando:

```bash
node -v
```

También se puede verificar la versión de npm:

```bash
npm -v
```

## **Instalar Node.js**

**Descargar NodeJS del sitio web**

```bash
https://nodejs.org/en
```
Proceder con la instalación

**Usar Node Version Manager (nvm)**

Instala nvm ejecutando el siguiente comando:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash
```

Cerrar y volver a abrir la terminal.

Luego cargar nvm:

```bash
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```

Instala la versión deseada de Node.js con nvm: 

```bash
nvm install --lts
```

 Verificar la instalación:

 ```bash
node -v
npm -v
 ```

## **Actualizar Node.js en macOS**

Hay varias formas de actualizar Node.js. 

### **Opción 1: Usar nvm (Node Version Manager)**
El **Node Version Manager (nvm)** es la mejor forma de gestionar versiones de Node.js. Permite instalar y cambiar entre diferentes versiones con facilidad.

**Instalar nvm**:
   Ejecuta este comando en tu terminal para instalar nvm:
   ```bash
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash
   ```

**Cerrar y reabrir la terminal**, o ejecuta este comando para cargar nvm:
   ```bash
   source ~/.bashrc  # O usa ~/.zshrc si usas zsh
   ```

**Verifica que nvm esté instalado**:
   ```bash
   nvm --version
   ```

**Actualizar Node.js**:
   - Ver todas las versiones disponibles de Node.js:
     ```bash
     nvm ls-remote
     ```
   - Instala la última versión estable:
     ```bash
     nvm install --lts
     ```
   - Cambia a la nueva versión instalada:
     ```bash
     nvm use --lts
     ```
   - Verifica la versión actual:
     ```bash
     node -v
     ```

### **Opción 2: Usar Homebrew**
Si ya usas **Homebrew** en tu Mac, es una forma rápida de instalar y actualizar Node.js.

Previamente: 

   Actualizar herramientas de linea de comandos de Xcode
   ```bash
   sudo rm -rf /Library/Developer/CommandLineTools
   sudo xcode-select --install
   ```
   También se puede descargar directamente de
   ```bash
     https://developer.apple.com/download/all/.

     You should download the Command Line Tools for Xcode 14.2.  
   ```

**Verifica si Homebrew está instalado**:
   ```bash
   brew --version
   ```
   Si no está instalado, puedes instalarlo con:
   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

**Actualizar Node.js con Homebrew**:
   - Actualiza Homebrew:
     ```bash
     brew update
     ```
   - Instala o actualiza Node.js:
     ```bash
     brew install node
     ```
     O si ya tienes Node.js instalado:
     ```bash
     brew upgrade node
     ```

**Verifica la versión actualizada**:
   ```bash
   node -v
   npm -v
   ```

## **Consejos para el manejo de Node.js en macOS**

- **Usar nvm si trabajas con múltiples proyectos**: Si trabajas con proyectos que necesitan diferentes versiones de Node.js, nvm es la mejor opción.
  
- **Verifica permisos**: Si alguna vez encuentras problemas de permisos al usar npm, puedes solucionarlo configurando un directorio global seguro:
```bash
mkdir ~/.npm-global
npm config set prefix '~/.npm-global'
export PATH=~/.npm-global/bin:$PATH
```

- **Limpieza de versiones antiguas**: Si usas nvm, puedes listar las versiones instaladas y eliminar las que ya no necesites:
```bash
nvm ls
nvm uninstall <version>
```


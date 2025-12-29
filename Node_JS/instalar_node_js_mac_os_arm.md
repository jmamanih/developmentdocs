# Instalación y Gestión de Node.js en macOS ARM (M1 / M2 / M3) usando NVM

Guía completa para instalar **Node.js** en **macOS con arquitectura ARM** utilizando **NVM (Node Version Manager)**. Incluye manejo de múltiples versiones, activación local y global, y comandos esenciales.


## ✅ Requisitos previos

### Verificar arquitectura
```bash
uname -m
```
Debe mostrar:
```
arm64
```

### (Opcional) Instalar Homebrew
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```


## 🔹 Instalación de NVM

### Método oficial recomendado
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```

O usando `wget`:
```bash
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```


## 🔹 Activar NVM

Después de la instalación, reinicia la terminal o ejecuta:

### Para ZSH (por defecto en macOS)
```bash
source ~/.zshrc
```

### Para Bash
```bash
source ~/.bashrc
```

Verificar instalación:
```bash
nvm --version
```


## 🔹 Instalar Node.js

### Instalar versión LTS (recomendada)
```bash
nvm install --lts
```

### Instalar versiones específicas
```bash
nvm install 18
nvm install 20
nvm install 22
```


## 🔹 Listar versiones instaladas
```bash
nvm ls
```

Ejemplo:
```
->     v20.11.1
       v18.20.3
       v16.20.2
default -> 20 (-> v20.11.1)
```

## 🔹 Usar una versión específica (temporal)
```bash
nvm use 18
```

Verificar:
```bash
node -v
npm -v
```

## 🔹 Establecer versión global por defecto
```bash
nvm alias default 20
```

## 🔹 Uso local por proyecto

Dentro del proyecto:
```bash
cd mi-proyecto
nvm use 18
```

### Uso automático con `.nvmrc`
```bash
echo "18" > .nvmrc
```

Luego ejecutar:
```bash
nvm use
```


## 🔹 Ver versión activa
```bash
node -v
```

```bash
which node
```

## 🔹 Desinstalar una versión
```bash
nvm uninstall 16
```

## 🔹 Ver versiones disponibles

### Todas las versiones
```bash
nvm ls-remote
```

### Solo LTS
```bash
nvm ls-remote --lts
```

## 🔹 Comandos útiles de NVM

| Acción | Comando |
|------|--------|
| Listar versiones instaladas | `nvm ls` |
| Listar versiones remotas | `nvm ls-remote` |
| Usar versión | `nvm use 20` |
| Instalar versión | `nvm install 20` |
| Versión por defecto | `nvm alias default 20` |
| Desinstalar versión | `nvm uninstall 18` |
| Ver versión de Node | `node -v` |
| Ver versión de npm | `npm -v` |

## 🔹 Verificar arquitectura de Node
```bash
node -p "process.arch"
```
Debe mostrar:
```
arm64
```

## 🔹 Ejemplo de uso en proyecto

```bash
mkdir proyecto-node
cd proyecto-node
nvm use 20
npm init -y
npm install express
```

## 🔹 Recomendaciones para macOS ARM

✔ Usar siempre Node **LTS**  
✔ No instalar Node con Homebrew si usas NVM  
✔ Usar `.nvmrc` por proyecto  
✔ Ideal para Laravel, React, Vite, Next.js






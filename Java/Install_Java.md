# Instalar Java en MacOs

Directorio de Instalación de versiones de Java

```sh
/Library/Java/JavaVirtualMachines
```

Instalar ultima version de Java

```sh
brew install java
```

## Instalar versiones de java con Temurin

Instalar con [Eclipse Temurin](https://adoptium.net/es/)

Buscar versiones disponibles
```sh
brew search temurin
```

Instalar version Java 17
```sh
brew tap homebrew/cask-versions
brew install --cask temurin17
```
Instalar ultima version

```sh
brew install --cask temurin
```

## Gestionar Versiones de Java con Jenv

### Instalar [jenv](https://www.jenv.be/)

```sh
brew install jenv
```

### Configurar Path de Jenv

En Bash

```sh
$ echo 'export PATH="$HOME/.jenv/bin:$PATH"' >> ~/.bash_profile
$ echo 'eval "$(jenv init -)"' >> ~/.bash_profile
```

En Zsh

```sh
echo 'export PATH="$HOME/.jenv/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(jenv init -)"' >> ~/.zshrc
```

### Adicionar versiones de Java con Jenv

```sh
jenv add /Library/Java/JavaVirtualMachines/jdk-11.0.1.jdk/Contents/Home/

jenv add /Library/Java/JavaVirtualMachines/temurin-17.jdk/Contents/Home/

jenv add /Library/Java/JavaVirtualMachines/temurin-21.jdk/Contents/Home/
```

### Listar versiones disponibles de Java

```sh
jenv versions
```

### Establecer version de Java a nivel Global

```sh
jenv versions
jenv global oracle64-11.0.1
```
cerrar terminal para ver el cambio

```sh
java --version
```
### Establecer version de Java a nivel Local (per directory)

Se puede establecer una version de Java en una carpeta determinada esta carpeta puede ser de un proyecto java

```sh
mkdir proyjava17
cd proyjava17
jenv local temurin64-17.0.9
java --version

    openjdk 17.0.9 2023-10-17

cd ..
java --version
    
    java 11.0.1 2018-10-16 LTS
```
### Establecer versión de Java a nivel de instancia de Terminal (shell instance version)

Se establece la versión de Java solo en la instancia de la terminal al cerrar la terminal se cambiara la version de Java a la versión global

```sh
jenv versions
jenv shell temurin64-21.0.1
```

cerrar terminal para volver a la versión global de java

# Instalar Maven

```sh
brew install maven
```

Ejecutar un proyecto java spring boot

```sh
 mvn spring-boot:run --debug
```
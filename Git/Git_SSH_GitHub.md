# Generar clave SSH en GitHub 

Cuando hay errores con la clave SSH (GitHub no está aceptando la llave pública). 
Solucion para entorno MacOs ARM


1️⃣ Verifica qué URL remota estás usando

Ejecuta en tu proyecto:

```sh
git remote -v
```

Debe verse algo como:

```sh
origin  git@github.com:usuario/repositorio.git (fetch)
origin  git@github.com:usuario/repositorio.git (push)
```

⚠️ Si ves https://github.com/..., entonces NO es SSH y este error no debería salir.
Si ves git@github.com, seguimos con SSH.


2️⃣ Verifica si ya tienes claves SSH

```sh
ls -al ~/.ssh
```
Busca archivos como:

```sh
id_rsa y id_rsa.pub
id_ed25519 y id_ed25519.pub
```
👉 Si NO existe ningún .pub, ir al paso 3.
👉 Si existe, ir al paso 4.


3️⃣ Crear una nueva clave SSH (recomendado: ed25519)

```sh
ssh-keygen -t ed25519 -C "tu_email@ejemplo.com"
```

Cuando pregunte:
    
    Enter para la ruta por defecto

Puedes poner passphrase o dejar vacío

Esto creará:

    ~/.ssh/id_ed25519
    ~/.ssh/id_ed25519.pub


4️⃣ Arranca el agente SSH y agrega la clave

```sh
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

Verifica que quedó cargada:

```sh
ssh-add -l
```

Debe mostrar algo como:

    256 SHA256:xxxxx id_ed25519


5️⃣ Agrega la clave pública a GitHub

Copia tu clave pública:

```sh
pbcopy < ~/.ssh/id_ed25519.pub
```
Luego en GitHub:

    Settings
    SSH and GPG keys
    New SSH key
    Pega la clave
    Guardar


6️⃣ Prueba la conexión con GitHub

```sh
ssh -T git@github.com
```

Respuesta correcta:

    Hi usuario! You've successfully authenticated, but GitHub does not provide shell access.


✅ Si ves esto → SSH funciona
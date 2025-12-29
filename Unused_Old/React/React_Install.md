# Instalación de React

Instalaciones previas:

- Node JS

Crear un proyecto React

```sh
mkdir sistram-app
cd sistram-app
npx create-react-app .
```

Otra forma de crear proyectos:

```sh
cd Projects
npx create-react-app sistram-app
```

Si salen errores al momento de crear el proyecto adicionar el parámetro "legacy-peer-deps"

```sh
npx create-react-app sistram-app --legacy-peer-deps
```

Cuando se crea el proyecto correctamente al final sale el mensaje "Happy hacking!"

*Nota:* los nombres de los proyectos no deben contener mayusculas, porque npm (Node Package Manager) no lo permite.

Ejecutar el proyecto:

```bash
cd sistram-app
npm start
```

Si sale el error: "Cannot find module 'ajv/dist/compile/codegen'"

Ejecutar la siguiente linea de comando:

```bash
npm install --save-dev ajv@^8
npm start
```

ó

```bash
npm install ajv@latest ajv-keywords@latest
```





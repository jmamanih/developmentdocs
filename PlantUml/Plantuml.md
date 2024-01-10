# PLANTUML
PlantUML es un componente versátil que permite crear diagramas de forma rápida y sencilla. Los usuarios pueden redactar una gran variedad de diagramas utilizando un lenguaje sencillo e intuitivo. Para profundizar en los detalles del lenguaje, consulte la Guía de referencia del lenguaje PlantUML.

Si es la primera vez que utiliza PlantUML, comience por la página de inicio rápido. Si tiene alguna duda, visite nuestra página de preguntas frecuentes. Integre PlantUML sin problemas dentro de muchas otras herramientas.

🧩 Diagramas UML soportados:

    Diagrama de secuencia
    Diagrama de casos de uso
    Diagrama de clases
    Diagrama de objetos
    Diagrama de actividades (Beta) (Encuentre aquí la sintaxis heredada)
    Diagrama de componentes
    Diagrama de despliegue
    Diagrama de estado
    Diagrama de tiempo

# Instalación

Instalacion del visor Plantuml en Visual Studio Code.

```sh
Open VSCode
Add Extension, PLantUml
Edit file with Plantuml code
Previsualization Panel: View
```
# Documentación

[Documentación](https://plantuml.com/es/)


# Errors

Dot Exetutable /opt/local/bin/dot Files does not exist. Cannot find Graphviz: You sould try
[error](/PlantUml/images/error_graphviz.png)

*Solve:*

```sh
brew install libtool
brew link libtool
brew install graphviz
brew link --overwrite graphviz
```

# Instalación de SonarQube

Instalación de SonarQube en Docker a través del plug-in Docker Compose.

<a href="https://github.com/EARodriguezM/SonarQube-Install/blob/main/README.md"><img src="https://img.shields.io/static/v1?label=&labelColor=505050&message=English README &color=%230076D6&style=flat&logo=google-chrome&logoColor=green" alt="website"/></a>

## Descripción del repositorio

El repositorio presenta la siguiente estructura 
``` bash
├── scripts
│   ├── install-sonar-scanner.sh
├── docker-compose.yml
├── README.md
├── README_es.md
```
Donde el archivo **install-sonar-scanner.sh** es un script ejecutable para la instalación de SonarScanner en los sistemas basados en Linux.

Por otro lado, el archivo **docker-compose.yml** es el utilizado para la instalación de las imágenes y levantamiento e inicio de los contenedores.

## Instrucciones
>
> Debe contar con el software Git instalado en su sistema.
>

### Windows

#### Instalar Desktop

Ir a la página de descarga [Docker Desktop](https://www.docker.com/products/docker-desktop/) descargar, ejecutar el archivo y seguir las instrucciones.

Luego de haber reiniciado el sistema, como lo requiere la instalación de Docker, se ejecutara el programa. (Si el software no inicia correctamente ir a [Problemas Solucionados](#Troubleshooting).

#### Ejecutar Docker Compose

A continuación, dirigirse al disco local de Windows (Normalmente el disco local `C:`) y crear una carpeta con nombre *SonarQube*, ingresar a dicha carpeta, y en la barra de direcciones escribir `CMD` para abrir la consola de comandos.

Ejecutar los siguientes comandos:

`git init`

`git pull https://github.com/EARodriguezM/SonarQube-Install`

`docker compose up -d`

Las líneas anteriores, descargaran los archivos de este repositorio en la carpeta creada, con la misma estructura explicada; descargaran las imágenes de SonarQube y PostgreSQL 12, desde los repositorios de Docker; y levantaran los respectivos contenedores.

#### Instalar SonarScanner

>
> El SonarScanner descargado en este apartado y en el link a continuación es el utilizado cuando no hay un escáner específico para su sistema de compilación (para JS, TS, Go, Python, PHP, ...). En caso de que su sistema este bajo [Maven](https://docs.sonarsource.com/sonarqube/latest/analyzing-source-code/scanners/sonarscanner-for-maven/), [Gradle](https://docs.sonarsource.com/sonarqube/latest/analyzing-source-code/scanners/sonarscanner-for-gradle/), [.NET](https://docs.sonarsource.com/sonarqube/latest/analyzing-source-code/scanners/sonarscanner-for-dotnet/), hacer clic en sus respectivos links.
>

Dirigirse a la documentación de SonarQube con el apartado [SonarScanner](https://docs.sonarsource.com/sonarqube/latest/analyzing-source-code/scanners/sonarscanner/) y descargar la versión **Windows-64-bit**. Esto descargará un archivo ZIP, el cual deberá ser descomprimido.

A continuación, deberá dirigirse a la carpeta de *SonarQube*, creada anteriormente, y crear una nueva carpeta llamada **scanner**. Copiar todo el contenido del archivo ZIP en la carpeta *scanner*.

Luego, se deberá entrar a la ventana de configuración de variables del entorno, y **Editar** o **Crear** la variable de usuario `Path`, donde agregara la siguiente dirección `C:\SonarQube\scanner\bin`, acepta la edición a la variable y cierra las ventanas.

#### Configurar SonarQube

Ingresar al puerto [local 9000](http://localhost:9000/) desde tu navegador e ingresar con las credenciales por defecto:

        Username = admin
        Password = admin

Luego de haber seteado una nueva contraseña, requerido por el aplicativo, se presentara la ventana para la creación de un nuevo proyecto.

#### Ejecutar Análisis: local

En la ventana para la creación de un nuevo proyecto, seleccionar *Manually* para la creación manual del proyecto. Se otorga un nombre al proyecto y un nombre a la rama por defecto, la *Project key* será establecida automáticamente por el software.

Próximamente, se redirige a la ventana para analizar el proyecto, en donde se seleccionara *Locally*. Se genera un nuevo toque haciendo clic en *Generate* y luego se presiona el botón *Continue*.

Seleccionar la opción que describe su sistema (es altamente relacionada con la versión de SonarScanner que tuvo que instalar), y seleccionar *Windows* como sistema operativo y copiar la línea de comando que aparece en la sección *Execute the Scanner* haciendo clic en el botón *Copy*.

Abrir `CMD` en la carpeta donde se encuentra el directorio raíz de su proyecto (donde usualmente se encuentra el archivo node_modules, package.json, lib, src, entre otros...) y ejecutar el comando copiado anteriormente.

>
> **NOTA**:Verificar que en la carpeta no debe haber dependencias instaladas, es decir, carpetas como `node_modules`, `build`, entre otras... No deben estar.
>

Durante la ejecución, se ejecutará una ventana emergente donde se le deberá otorgar permisos de red a Sonar para la comunicación de datos entre *SonarScanner* y *SonarQube*.

Terminada la ejecución, el navegador actualizara y presentara los valores del análisis.


## <a name="Troubleshooting"></a> Problemas Solucionados
- https://stackoverflow.com/a/68768646
- https://stackoverflow.com/a/61191886
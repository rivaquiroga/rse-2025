# Buenas prácticas de programación para proyectos de investigación

Este taller tiene por objetivo abordar algunas de las habilidades fundacionales que usualmente se requieren al trabajar con software para investigación. En particular, pondremos el foco en buenas prácticas de programación que favorecen la reproducibilidad. Se cubrirán temas como el uso de la línea de comandos para la gestión de archivos y automatización de tareas, el control de versiones con Git + GitHub, así como estrategias para asegurar la calidad y reproducibilidad de nuestros flujos de análisis de datos con Python y R.

## Preparación
A continuación se indican los programas y aplicaciones que es necesario instalar antes del taller. Todas son herramientas bastantes extendidas, por lo que ante cualquier duda siempre es posible encontrar algún tutorial en YouTube con el paso a paso de la instalación. Los paquetes y librerias que usaremos las instalaremos durante el taller.

### Instalar Bash
Si usas Linux o MacOS, Bash viene por defecto, así que no tienes que hacer nada. Si usas Windows, puedes instalarlo a través de Git Bash (y así te queda instalado Git, que es el siguiente paso): https://gitforwindows.org/. 

Si usa macOS por defecto viene zsh. Los comando funcionan igual. Si quieres cambiarte a Bash, ejecuta esto en tu Terminal:

```
chsh -s /bin/bash
```
Luego tienes que cerrar y volver a abrir la Terminal para que se actualice.

### Instalar Git
Si usas MacOS, Git debería venir instalado. De todos modos, puedes chequear ejecutando en la Terminal lo siguiente

```
git --version
```

Si no lo tienes, puedes elegir alguna de las opciones que se muestran en la página de Git: https://git-scm.com/downloads/mac.

Si usas Windows, Git debería haber quedado instalado en el paso anterior al instalar Bash. Si no, puedes revisar las indicaciones en la página de Git: https://git-scm.com/downloads/win

### Crear una cuenta en GitHub
Si todavía no tienes una cuenta en GitHub (el sitio en que estás mirando esto ahora), créate una. Te sugerimos pensar bien tu nombre de usuario, porque cambiarlo después hace que algunas cosas se rompan o se comporten de forma inesperada. 

### Instalar/actualizar R 
Instala la versión más reciente de R desde https://cran.r-project.org/.
Personas que usan Windows: además de instalar la opción que dice base, instalen la que dice RTools

### Instalar/actualizar RStudio
Instala RStudio desde https://posit.co/download/rstudio-desktop/

### Crear una cuenta en Posit Cloud
Posit Cloud es el servicio en la nube de Posit, la empresa que desarrolla RStudio: https://posit.cloud/

### Instalar/actualizar Python
Puedes descargar la versión mås reciente de Python desde https://www.python.org/downloads/release/python-3131/. Si usas Windows, instala la versión que dice "Recommended".

### Instalar/actualizar VSCode
Puedes decargarlo desde https://code.visualstudio.com/

## Materiales

### Ejercicio 1. Bash

Los datos están disponibles en Figshare: <https://doi.org/10.6084/m9.figshare.13040516>. Hay que descargar la carpeta comprimida, descomprimirla y llamarla `data`. Esa carpeta la guardaremos dentro del directorio raíz de nuestro proyecto, que se llamará `zipf`. Es decir, debería quedar la siguiente estructura en tu computador:

```
zipf/
  ├── data
      ├── dracula.txt
      ├── frankenstein.txt
      ├── jane_eyre.txt
      └── ...
```
La sugerencia es que dejen esto en el escritorio de su computador para que sea más fácil encontrarla.

Material de apoyo: libro online [Research Software Engineering with Python](https://third-bit.com/py-rse/).

### Ejercicio 2. Bash

Descarga [este directorio](https://www.dropbox.com/s/nik8cwkme2yw4hl/archivos.zip?dl=0) y descomprímelo en tu escritorio. Para que nos quede todo más ordenado, la sugerencia es que esta sea tu estructura de carpetas:

```
Escritorio/
  ├── taller/
      ├── archivos/
      ├── zipf/
      └── ...
```
Para este ejercicio crearemos una carpeta que se llame `carpeta-compartida` que debe quedar en el primer nivel dentro de la carpeta `taller`:

```
Escritorio/
  ├── taller/
      ├── archivos/
      |── carpeta-compartida/
      ├── zipf/

```

Si estás en la terminal ubicada dentro de la carpeta taller, puedes crearla directo con `mkdir carpeta-compartida`. Si estás más arriba o más abajo, tendrías que editar la ruta.

## Ejercicio 3. Bash + un lenguaje de programación

Crearemos una nueva carpeta que se llamará `tiempo`:

```
Escritorio/
  ├── taller/
      ├── archivos/
      |── carpeta-compartida/
      |── tiempo/
      ├── zipf/
```

Descarga este [script de R](https://www.dropbox.com/scl/fi/qh1zyd1pxx1enz43ompyp/arreglar-formato-valores.R?rlkey=sh2v0jtpa5ad7g267r0wxcwww&dl=0) y estos [datos](https://www.dropbox.com/scl/fi/vlqyeavjcfzp88q6of2ms/santiago_temperatura.csv?rlkey=1l8rehg5rlay27mv6rg801mly&dl=0) y guárdalos en la carpeta tiempo.

## Ejercicio 4. Ambiente virtual en Python

Guardaremos dos copias de [este archivo](https://www.dropbox.com/scl/fi/92752gegfy73hvd63hz4y/01_extraccion-tablas.py?rlkey=ywk250qw9hizjy1eqks5xtzum&dl=0): una en la carpeta ambiente-python y otra en ambiente-test. 

Primero creamos el ambiente virtual:
* `python3 -m venv ambiente-virtual` y luego, lo activamos con `ambiente-virtual\Scripts\activate` en Windows y `source ambiente-virtual/bin/activate` en macOS/Linux.
* También lo podemos crear y activar a través de la paleta de comandos en VS Code con ctrl + mayúscula + P y luego buscando "ambiente". Elegimos venv y luego la versión más reciente de Python.

Luego, instalamos las librerías que necesita el código: 
```
pip install requests
pip install bs4
pip install pandas
```

Si compartimos nuestro código con otras personas podemos guardar la información de las librerías que tenemos instaladas con `pip freeze > requirements.txt`. Luego, ellas pueden usar `pip install -r requirements.txt` para que se le instalen en su entorno virtual las mismas versiones de cada librerías. 

## Ejercicio 5. Código reproducible, sessionInfo(), renv

Primero, en parejas o tríos, exploraremos el código de este proyecto de R disponible en Posit Cloud: https://posit.cloud/content/9592938. 
Luego, descargaremos el proyecto y veremos qué pasa cuando lo tratamos de ejecutar localmente. 
Es necesario que tengas instalados los siguientes paquetes para poder ejecutar el código en tu computador: guaguas, dplyr, ggplot2, ggthemes. Puedes instalarlos todos con `install.packages(c("guaguas", "dplyr", "ggplot2", "ggthemes"))`
¿Por qué los resultados son diferentes?

## Ejercicio 6

En la terminal, nos ubicaremos en la carpeta taller y ejecutaremos la siguiente línea de código:

```
git clone https://github.com/rivaquiroga/ejemplo-extraccion-github-actions.git
```
En Linux y Windows, para pegar texto en la terminal es necesario usar **ctrl + mayúsculas + V**.

Esto creará una copia de un repositorio que está en GitHub de forma local en su computador. El repositorio no tiene documentación. Lo analizaremos para ver qué podríamos describir para que sea más fácil utilizarlo en el futuro. Y de pasada, hablaremos de GitHub Actions.


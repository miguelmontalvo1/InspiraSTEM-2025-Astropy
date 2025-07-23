# Instrucciones de Instalación y Configuración para el Taller

Para ejecutar todos los notebooks del taller en tu propia computadora, asegúrate de que tu máquina esté configurada con los paquetes especificados en el [archivo de verificación de instalación](https://github.com/astropy/astropy-workshop/blob/main/00-Install_and_Setup/). Estos paquetes son los que usamos para verificar que los notebooks funcionen correctamente.

Estas instrucciones describen cómo configurar el entorno usando `git` y `Miniforge`. No es estrictamente necesario usar estos programas. Consulta la sección [Métodos Alternativos de Instalación](#alternate-installation-methods) al final de este documento.

Si tienes problemas con alguno de los pasos, revisa si ya han sido reportados en el [rastreador de problemas](https://github.com/astropy/astropy-workshop/issues/). Si no es así, [haz tu pregunta en el rastreador de problemas](https://github.com/astropy/astropy-workshop/issues/new?assignees=&labels=workshop-question&template=question-from-workshop-participant.md&title=%5BQuestion%5D+Resume+tu+pregunta+aquí). También puedes [unirte al Slack de Astropy] y preguntar en el canal `#workshops`.

En los comandos que se muestran a continuación, `%` (y todo lo que está a la izquierda) representa el prompt de la terminal. No necesitas copiarlo; solo copia el comando que aparece a la derecha.

## 0. (Solo para Windows) Instalar WSL

*Si estás usando Windows, recomendamos utilizar el Subsistema de Windows para Linux (WSL) en lugar de herramientas nativas de Windows. WSL ahora es totalmente compatible con Microsoft, suele generar menos problemas de instalación, y permite utilizar herramientas desarrolladas para Linux directamente en Windows. Aunque aún puedes usar la instalación nativa de Miniforge en Windows, estas instrucciones se centran en WSL por las razones mencionadas.*

Para instalar WSL, sigue las instrucciones que Microsoft proporciona aquí: https://docs.microsoft.com/en-us/windows/wsl/install. Aunque puedes elegir una distribución de Linux diferente a Ubuntu, las instrucciones han sido probadas con Ubuntu, así que te sugerimos usar esa a menos que tengas una razón específica.

*Opcional:* Aunque puedes ejecutar WSL desde el símbolo del sistema de Windows, es bastante limitado. Te recomendamos [instalar Windows Terminal](https://docs.microsoft.com/en-us/windows/terminal/install) para una mejor experiencia, más similar a Mac o Linux. También puedes consultar [Configurar un entorno de desarrollo con WSL](https://learn.microsoft.com/en-us/windows/wsl/setup/environment).

## 1. Instalar Miniforge (si es necesario)

*Miniforge es un instalador minimalista y gratuito para conda. Incluye solo conda, Python, los paquetes que dependen de ellos y algunos otros útiles como pip, zlib, entre otros. También usa por defecto el repositorio conda-forge, que contiene un conjunto más amplio de paquetes con licencias abiertas (a diferencia de Anaconda o Miniconda). Si ya tienes Miniforge, miniconda o Anaconda instalado, puedes pasar al siguiente paso.*

En una terminal, verifica si Miniforge o algún instalador similar ya está instalado:

    % conda info

Si conda no está instalado, sigue las instrucciones correspondientes a tu sistema operativo:  
https://github.com/conda-forge/miniforge/blob/main/README.md

Si estás usando Windows, ejecuta el instalador *para Linux* dentro de una terminal WSL, en lugar de usar el instalador para Windows.

(En Windows nativo, podrías necesitar [compiladores adicionales](https://github.com/conda/conda-build/wiki/Windows-Compilers), aunque esto no debería ser necesario si usas WSL).

## 2. Abrir la terminal de conda

*Miniforge incluye un administrador de entornos llamado conda. Los entornos permiten tener múltiples conjuntos de paquetes de Python instalados al mismo tiempo, lo cual facilita la reproducibilidad y las actualizaciones. Puedes crear, exportar, listar, eliminar y actualizar entornos que tengan diferentes versiones de Python y/o diferentes paquetes instalados. Para este taller, configuraremos el entorno usando la terminal de conda.*

Abre una terminal y verifica que conda esté funcionando correctamente:

    % conda info

Si tienes problemas, verifica qué shell estás utilizando en tu terminal con:

    % echo $SHELL

Luego, si es necesario, ejecuta la inicialización en esa misma terminal:

    % conda init `basename $SHELL`

Después de ejecutar `conda init`, debes abrir una nueva ventana de terminal.

Es recomendable actualizar conda a su versión más reciente. Sugerimos una versión mínima de 23.10.0. Para verificar tu versión de conda:

    % conda --version

Actualízalo con:

    % conda update conda

o también puedes usar:

    % conda update -n base conda


## 3. Instalar git (si es necesario)

En la terminal que abriste en el paso anterior, ejecuta el siguiente comando para verificar si git ya está instalado y accesible desde esta terminal:

    % git --version

Si la salida muestra una versión de git, puedes continuar con el siguiente paso. De lo contrario, instala git ejecutando el siguiente comando y siguiendo las instrucciones que aparezcan:

    % conda install git

## 5. Clona este repositorio o descarga un archivo ZIP

Si estás usando `git`, clona el repositorio del taller utilizando  
[git](https://help.github.com/articles/set-up-git/):

    % git clone https://github.com/miguelmontalvo1/InspiraSTEM-2025-Astropy

Si decides no usar `git`, puedes descargar el archivo ZIP haciendo clic en el botón verde *Code* en  
https://github.com/miguelmontalvo1/InspiraSTEM-2025-Astropy y seleccionando *Download ZIP*.

## 6. Crear un entorno conda para el taller

*Miniforge incluye un administrador de entornos llamado conda. Los entornos permiten tener múltiples conjuntos de paquetes de Python instalados al mismo tiempo, lo cual facilita la reproducibilidad y las actualizaciones. Puedes crear, exportar, listar, eliminar y actualizar entornos que tengan diferentes versiones de Python y/o distintos paquetes instalados.*

Crea un entorno conda para este taller utilizando un archivo `.yml`.  
La versión de Python está especificada en el archivo  
[environment.yml](https://github.com/astropy/astropy-workshop/blob/main/00-Install_and_Setup/environment.yml).

Abre una ventana de terminal apropiada para tu sistema operativo.

Ahora navega a este directorio en la terminal. Por ejemplo, si instalaste el directorio `astropy-workshop` en tu carpeta personal, podrías escribir lo siguiente:

    % cd InspiraSTEM-2025-Astropy/00-Install_and_Setup/

Y finalmente, en cualquier plataforma, para instalar y activar el entorno `astropy-workshop`, escribe:

    % conda env create --file environment.yml
    % conda activate astropy-env

Nota: necesitarás conda versión 23.10.0 o posterior. Si necesitas actualizar tu versión, usa `conda update conda`.

El nombre del nuevo entorno conda creado debería aparecer junto al prompt de la terminal:  
`(astropy-env) %`

Todos los paquetes necesarios están especificados en el archivo  
[requirements.txt](https://github.com/astropy/astropy-workshop/blob/main/00-Install_and_Setup/requirements.txt).  
Instálalos con el siguiente comando:

    (astropy-env) % pip install -r requirements.txt

## 7. Verificar la instalación

El nombre del nuevo entorno conda creado debería aparecer junto al prompt de la terminal:  
`(astropy-env) %`

En la terminal que usaste en el paso anterior, dentro del directorio  
`InspiraSTEM-2025-Astropy/00_Install_and_Setup/`, ejecuta el script `check_env.py`  
para verificar el entorno de Python y algunas de las dependencias requeridas:

    (astropy-env) % python check_env.py

Si el script indica que algunas versiones no coinciden, primero verifica si el paquete fue instalado con conda o con pip, y actualízalo según corresponda.  
En el ejemplo a continuación se usa un paquete ficticio llamado `packagename`; reemplázalo por el nombre del paquete que necesitas actualizar.

    (astropy-env) % conda list packagename

Si fue instalado con conda, verás algo así (la columna de canal puede estar o no poblada):

    # packages in environment at .../miniforge/envs/astropy-env:
    #
    # Name                    Version                   Build  Channel
    packagename               X.Y.Z         py37hf484d3e_1000

De lo contrario, si fue instalado con pip, verás que la columna de canal indica el nombre `pypi`:

    # packages in environment at .../miniforge/envs/astropy-env:
    #
    # Name                    Version                   Build  Channel
    packagename               X.Y.Z                     pypi_0    pypi

Para actualizar el paquete reportado usando conda:

    (astropy-env) % conda update packagename

De lo contrario, para actualizar con pip:

    (astropy-env) % pip install packagename --upgrade

La excepción a esto es si el paquete `astroquery` aparece como desactualizado; siempre actualízalo a su versión pre-lanzamiento usando pip:

    (astropy-env) % pip install astroquery --pre --upgrade

## 8. Iniciar Jupyter Notebook

En la ventana de terminal que usaste con el entorno conda creado anteriormente,  
cambia el directorio al nivel raíz del directorio `nspiraSTEM-2025-Astropy`.

    (astropy-env) % cd ..

Asegúrate de que el directorio actual en tu terminal contenga todos los directorios numerados de los notebooks.  
Luego, inicia Jupyter Notebook con el siguiente comando:

    (astropy-env) % jupyter notebook

Si todo sale bien, tu navegador abrirá una nueva pestaña o ventana apuntando a localhost y mostrará un listado del directorio incluyendo todas las subcarpetas numeradas de los notebooks.

Haz clic en una de las carpetas de notebooks, como `02-PythonIntro`.
Luego haz doble clic en un notebook, por ejemplo `01. Números, Cadenas de Texto y Listas`, y espera a que se abra.

En la esquina superior derecha, si ves que aparece y desaparece el mensaje azul "Kernel Ready", todo está bien.
Sin embargo, si ves un mensaje rojo "Kernel Error", haz clic sobre él y desplázate hacia abajo para ver el mensaje de error.
Si dice `FileNotFoundError`, detén el servidor del notebook en tu terminal y ejecuta este comando:

    (astropy-env) % python -m ipykernel install --user

Ahora, intenta ejecutar `jupyter notebook` nuevamente como se mostró antes, y el error de kernel debería desaparecer.  
Para asegurarte, ejecuta la primera celda (usualmente un `import`) y verifica que se ejecute correctamente.

Además, para confirmar que el notebook está utilizando `astropy` desde el entorno correcto, crea una nueva celda en el notebook (usa el botón `+` en el menú superior) y ejecuta el siguiente código:

    import astropy
    print(astropy.__version__)

Si la versión reportada de `astropy` es más antigua de lo esperado y no has ejecutado el comando `python -m ipykernel install --user`, entonces ejecútalo según las instrucciones anteriores.

## Métodos Alternativos de Instalación

Aunque recomendamos Miniforge, puedes usar `pip install -r requirements.txt` en una instalación de Python existente, o crear un entorno virtual usando [pip/venv](https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/).

## Recursos Adicionales

- [Configurar git](https://help.github.com/articles/set-up-git/)
- [Guía de usuarios de Conda](https://docs.conda.io/projects/conda/en/latest/user-guide/)
- [Instrucciones de instalación de Astropy](http://docs.astropy.org/en/latest/install.html)

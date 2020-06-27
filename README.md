# Curso práctico de Git y Github nivel básico
En este curso básico, aprenderás los conceptos fundamentales de Git y su integración con Github, para que puedas comenzar a utilizarlo en tus proyectos.
## Introducción
- Git es un controlador de versiones distribuido, de código abierto, que se utiliza para llevar el control de cambios en un proyecto de software. Fue creado por Linus Torvalds, quien también creó el kernel de Linux.
- Github es una plataforma para llevar el control de repositorios online. Nos permite crear repositorios públicos y privados, clonarlos, trabajar en equipos de desarrollo, etc. Github es propiedad de Microsoft.
- Algunas alternativas a Github son: 
 - [GitLab](https://about.gitlab.com/)
 - [Bitbucket](https://bitbucket.org/)
 - [SourceForge](https://sourceforge.net/)
### Principales características de Git
- Distribuido: toda persona que trabaja en el repositorio tiene un backup completo del mismo, no hay un sistema central. La única manera de que se pierda el trabajo de un proyecto es si existe solo una copia del mismo
- Gratuito y de código abierto. [Repo github](https://github.com/git/git)
- Veloz: dado que la mayoría de operaciones en Git se realizan de manera local, y a que está escrito primordialmente en C, Git es sumamente veloz, incluso al trabajar con proyectos muy grandes
- Flexible: por su naturaleza distribuida, Git permite utilizar cualquier modo de trabajo que se ajuste a las necesidades del proyecto o equipo de desarrollo
## Configuración básica
- Antes de comenzar a trabajar con Git, te recomiendo que configures tu nombre y correo electrónico. Esto para identificar los cambios que realices en un repositorio.
- ```git config --global user.name "[nombre]"```
- ```git config --global user.email "[email]"```
## Repositorios
Un repositorio es el 'almacén' en el cual se guardará nuestro código, puede contener cualquier cantidad de archivos y carpetas, y estos archivos pueden tener diferentes extensiones. Es en este repositorio en donde Git se encargará de controlar las diferentes versiones de nuestro proyecto, las cuales podemos acceder en cualquier momento que deseemos.
### Local vs remoto
#### Local
- Un repositorio local es aquel que está almacenado en nuestro ordenador
- Para crear un repositorio local, utilizamos el comando ```git init```
- Este comando creará un directorio oculto llamado ```.git```
#### Remoto
- Un repositorio remoto está almacenado en un servidor externo, ya sea en internet o en una red local
- Los repositorios remotos son la norma al trabajar en un proyecto en el cual se involucran varias personas
- Podemos crear un repositorio local a partir de un repositorio remoto, teniendo la URL del repositorio remoto. A este proceso se le conoce como *clonar*, y para hacerlo se utiliza el comando ```git clone <url_repo_remoto>```
- La mayoría del trabajo lo realizaremos en nuestra copia o nuestro clon de este repositorio remoto
- Un repositorio remoto contiene únicamente las diferentes versiones de nuestro código, no es posible realizar cambios directamente al mismo sin haberlo clonado antes, y haber publicado los cambios
## *Working Tree*
En el momento en que tengamos un repositorio en nuestro ordenador, ya sea al haberlo creado localmente o haber clonado uno existente, tendremos un *working tree*. Este concepto se refiere a un directorio en nuestro ordenador que está asociado a un repositorio. Para saber cuál es el estado del *working tree*, utilizamos el comando ```git status```.
## [*Stage*](https://dev.to/sublimegeek/git-staging-area-explained-like-im-five-1anh)
En nuestro *working tree* podemos realizar diferentes tipos de cambios: agregar, eliminar o modificar archivos y directorios. El *stage* es el conjunto de cambios que deseamos incluir **antes** de que pasen a formar parte del repositorio . Estos cambios **aun no son finales**, y podemos sacarlos del área de *stage* cuantas veces queramos. 
### Agregar y eliminar archivos de stage
- Para agregar un archivo al *stage*, utilizamos el comando ```git add <nombre_archivo>```
- Para eliminar un archivo del *stage*, utilizamos el comando ```git rm <nombre_archivo>```
## *Commit*
Después de que hayamos realizado cambios en el área de *stage*, podemos **confirmar** dichos cambios y guardarlos en el repositorio, mediante el comando ```git commit```. Al realizar esta operación, nuestra área de *stage* estará vacía nuevamente, pues los cambios han pasado a formar parte del repositorio de manera oficial.
- Para realizar un *commit*, utilizamos el comando ```git commit -m "<mensaje commit>``` o ```git commit```, que nos llevará a un archivo con el resumen de nuestros cambios, en ella debemos incluir el mensaje con la descripción de los mismos.
- ```git commit -a```: Agregar de manera automática al *stage* y al *commit* los archivos que hayan sido modificados o eliminados. Aplica únicamente para archivos ya existentes.
### Ignorar archivos
Es común que haya archivos y directorios en nuestro proyecto que no queramos monitorear, como archivos de *build*, archivos del sistema, dependencias externas, etc. Git nos permite esta funcionalidad con ayuda del archivo ```.gitignore```. En este podemos indicar archivos específicos a ignorar, directorios, extensiones. [ejemplo](https://github.com/facebook/create-react-app/blob/master/.gitignore). Estos archivos no formarán parte de nuestra área de *stage*, por lo tanto tampoco del *commit* ni del repositorio.
### Inspeccionar un commit
Para revisar a detalle los cambios realizados en un *commit*, utilizamos el comando ```git show <hash>```
## [Ramas](https://www.atlassian.com/git/tutorials/using-branches)
- Una rama o *branch* es una 'línea' de desarrollo independiente.
- Cuando trabajamos en un feature o hotfix, creamos una rama a partir de la rama principal, conocida como *master*. Podemos crear ramas a partir de cualquier otra rama, no tiene que ser necesariamente desde *master*
> Nota: En junio de 2020, Github anunció que cambiará el nombre de la rama *master* para evitar referencias a la esclavitud. A día de hoy, aun no se sabe cuál será el nuevo nombre. Más info [aquí](https://www.linuxadictos.com/github-y-otros-proyectos-eliminaron-la-terminologia-maestro-y-esclavo.html) 
### Creación de ramas
- Para crear una rama, utilizamos el comando ```git branch <nombre_rama>```
### Moverse entre ramas
- Para movernos a una rama, utilizamos el comando ```git checkout <nombre_rama>```
- Podemos crear una rama y movernos automáticamente a la misma mediante el comando ```git checkout -b <nombre_rama>```
### Listado de ramas
- Para ver todas las ramas en nuestro repositorio, utilizamos el comando ```git branch```. Un `*` aparecerá a lado de nuestra rama actual
### *Log*
- Para examinar la lista completa de *commits* incluídos en nuestra rama actual, utilizamos el comando ```git log```
## Trabajar con repositorios remotos
Antes vimos qué es un repositorio remoto y cómo clonar uno. En esta sección aprenderemos las operaciones más comunes al trabajar con repos remotos: push, pull y pull request. 
### *Remote*
Git nos permite indicar una o más URLs de un repositorio/repositorios remoto(s) que queremos asociar a nuestro repositorio local. A esta configuración se le conoce como *remote*. Al clonar un repositorio, el *remote* se configura automáticamente, y Git le asigna el nombre de *origin*. Para saber cuál es nuestra configuración de *remote*, utilizamos el comando ```git remote -v```
#### Asociar un repositorio local a un repositorio remoto
Es común que estemos trabajando en un repositorio local y decidamos guardar nuestro trabajo también en un repositorio remoto. Para esto hay que seguir los siguientes pasos:
1. Guardar nuestro trabajo local con un *commit*
2. Crear un repositorio remoto en Github o alguna otra plataforma
3. Configurar el *remote* a la URL del repositorio que creamos, mediante el siguiente comando:
```bash
git remote add <nombre_remote> <url_repo>
# La norma es utilizar 'origin' como el nombre remoto, pero puedes usar el nombre que quieras
```
##### git push
Hasta este paso, ya le hemos indicado a Git cuál es el nombre de nuestro repositorio remoto y su URL, pero no hemos enviado nuestros cambios. Para ello utilizamos el comando ```git push```
4. Enviar nuestros cambios
```bash
git push -u <nombre_remote> <nombre_rama>
```
- La bandera ```-u / --set-upstream``` guarda nuestra configuración de upstream, que consiste en el *remote* y la rama, para que la siguiente vez que utilicemos el comando solo tengamos que escribir ```git push```. Esta configuración también aplica para el comando ```git pull```.
- Con estos pasos nuestros cambios se encontrarán en el repositorio remoto que hayamos configurado
##### git pull
- La operación 'opuesta' a *push* es ```git pull```, que obtiene los cambios remotos y los integra a nuestro repositorio local
- Si no existe una configuración de *upstream* para la branch en la que estemos trabajando, el comando ```git pull``` no funcionará. Para configurar el upstream en una rama, podemos utilizar cualquiera de los dos siguientes comandos:
```bash
git branch -u <upstream>
git branch --set-upstream-to=<upstream>
# Recuerda que ```git push -u``` también guarda esta configuración
```
- Si deseas saber si tienes un *upstream* configurado, utiliza el comando ```git branch -vv```, que enlistará el *upstream* (si es que existe) de todas las ramas en tu repositorio
- Si queremos realizar un pull a un *upstream* distinto al que tenemos configurado, podemos utilizar el siguiente comando:
```bash
git pull <nombre_remote> <nombre_rama>
# Este comando **no** guarda la configuración de *upstream*
```
> Nota: Es bueno saber que, internamente, ```git pull``` ejecuta los comandos ```git fetch``` y ```git merge```. El primero obtiene los cambios remotos y el segundo los integra a nuestra rama actual 
## git merge
### Resolver conflictos
## Pull request
## EXTRAS
### Gitflow
### Herramientas gráficas para trabajar con git: Github Desktop, Sourcetree, etc

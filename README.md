<h1 align="center">Entendiendo Git</h1>

<img src="https://miro.medium.com/max/5000/0*a2jcqSzpTl6HQp35">

## Tabla de Contenido

- [1. Configurando Git](#)
- [2. Fundamentos de Git](#)

# 1. Configurando Git

Vamos a personalizar nuestro entorno y será necesario hacerlo solo una vez. Se puede cambiar la configuración después ejecutando los comandos correspondientes.

`git config` permite obtener y establecer variables de configuración que controlan el aspecto y funcionamiento de Git.

Estas variables pueden almacenarse en 3 lugares:

1. `/etc/gitconfig`: archivo de configuración de todos los usuarios del sistema. 
    - Usamos `git config --system` para leer o modificar este archivo:
    ```bash
    git config --system -l ## ver los valores del archivo (-l: --list)
    git config --system -e ## editar el archivo (-e: --?)
    ```
2. `~/.gitconfig` o `~/.config/git/config`: archivo de configuración del usuario actual del sistema. 
    -  Usamos `git config --global` para leer o modificar este archivo:
    ```bash
    git config --global -l ## ver los valores del archivo
    git config --global -e ## editar el archivo
    ```
3. `.git/config`: archivo de configuración del repositorio actual.

Cada nivel sobrescribe los valores del nivel anterior, por lo que los valores de `.git/config[3]` tienen preferencia sobre los de `/etc/gitconfig[1]`.

## 1.1. Estableciendo nuestro editor

Por ejemplo, en el archivo de configuración `--system` está establecido el editor que selecionamos durante la instalación de Git y esta configuración afecta a todos los usuarios del sistema. Podríamos establecer otro editor en la configuración `--global` para que afecte solo a nuestro usuario de sistema. En este caso estableceremos **VSCode** como editor:
```bash
git config --global core.editor code
```
## 1.2. Estableciendo nuestra identidad

Lo primero que debemos hacer cuando instalamos Git es establecer nuestro nombre y email. Esto es importante porque esta información es introducida en los commits que envíamos.
```bash
git config --global user.name "Cristian Flores"
git config --global user.email cristianflores.ee@gmail.com
```
Para sobrescribir esta información en proyectos específicos, debemos ejecutar el comando sin el flag `--global` estando en el proyecto a configurar.
```bash
git config user.name "Andrés"
```
## 1.3. Estableciendo alias para nuestros comandos

Podemos añadir alias en la configuración.
```bash
git config --global alias.l "log --oneline --decorate --all" # 'l' es el alias
git config --global alias.s "status -s -b" # 's' es el alias
```

## 1.4. Comprobando nuestra configuración

Podemos usar el comando `git config --list` para mostrar todas las propiedades que Git ha configurado.
```bash
$ git config --list
user.name=Cristian Flores
user.email=cristianflores.ee@gmail.com
color.status=auto
color.branch=auto
color.interactive=auto
color.diff=auto
...
```

Puede que veamos claves repetidas porque Git lee la misma clave de distintos archivos (por ejemplo, `/etc/gitconfig` y `~/.gitconfig`). En estos casos, Git usa el último valor para cada clave única que ve.

Para comprobar el valor que Git utilizará en una clave específica ejecutamos `git config <KEY>`:
```bash
$ git config user.name
Cristian Flores
```

## 1.5. Obteniendo ayuda

Existen 3 formas de ver la página del manual para cualquier comando:
```bash
$ git help <VERB>
$ git <VERB> --help
$ man git-<VERB>
```
Ejemplo:
```bash
git help config
```
Podemos acceder a los manuales incluso sin conexión a internet.

# 2. Fundamentos de Git

## 2.1. Los 3 estados

Estados en los que se pueden encontrar nuestros archivos:
1. **commited:** almacenado de manera segura en nuestra db local.
2. **modified:** modificado pero todavía no confirmado a nuestra db local.
3. **staged:** marcado para que se vaya en el próximo commit.

Secciones de un proyecto Git:
1. **git directory (.git):** almacena metadatos y db para nuestro proyecto. Es lo que se copia cuando clonamos un repositorio.
2. **working directory:** copia de una versión del proyecto. Esta se saca de la db comprimida en el `git directory`, y se coloca en disco para poder usarla.
3. **staging area:** archivo en tu `git directory`, que almacena info de lo que irá en nuestro próximo commit.

El flujo de trabajo básico en Git sería algo como:
1. Modificas archivos en tu `working directory`.
2. Preparas los archivos añadiendolos al `staging area`.
3. Confirmas los cambios, lo que toma los archivos tal como están en el `staging area` y los almacena de manera permanente en tu `git directory`.

<img src="https://i.imgur.com/7i9c2UK.png">

Adicionalmente:
+ Si una versión concreta de un archivo está en el `git directory` se considera `commited`.
+ Si se ha modificado desde que se obtuvo del repo, pero ha sido añadida al `staging area`, está `staged`.
+ Si se ha modificado desde que se obtuvo del repo, pero no se ha añadido al `staging area`, está  `modified`.

# 2. Obteniendo un repositorio

## 2.1. Inicializando un repositorio
Para iniciar el seguimiento de un proyecto con Git, debemos dirigirnos al directorio del proyecto y ejecutar:
```bash
git init
```

Esto creará un subdirectorio `.git` que contiene todos los archivos necesarios del repositorio, entre ellos una db comprimida.

## 2.2. Clonando un repositorio

El comando `git clone` nos permite descargar el repositorio con cada una de las versiones del proyecto.
```bash
git clone <URL>
```
Ejemplo:

```bash
git clone https://github.com/floxcristian/learn_git
```
Este comando crea un directorio `learn_git` y un subdirectorio `.git`, descarga toda la información del repositorio y envía una copia al `working directory` de la última versión.

De este manera, si el servidor se cae o tiene algun inconveniente, podemos usar cualquiera de los clones para devolver el servidor al estado en el que estaba cuando fue clonado.

Para especificar un nombre distinto al del repositorio:
```bash
git clone https://github.com/floxcristian/learn_git my_repo
```
# 3. Guardando cambios en el repositorio

Vamos a realizar cambios y confirmar instantáneas de esos cambios en el repositorio cada vez que se alcance un estado que queramos conservar.

Cada archivo del repositorio puede tener 2 estados:
+ **tracked:** archivos que estaban en la última instantánea del proyecto. Pueden ser archivos sin modificar, modificados, o preparados (`staged`).
+ **untracked:** archivos en el `working directory` que no estaban en la última instantánea y no están en el `staging area`.

Ciclo de vida del estado de tus archivos:
+ Cuando clonas un repositorio todos los archivos estarán `tracked` y sin modificar. 
+ Mientras editas, Git los ve como modificados (han sido cambiados desde su último commit).
+ Luego preparas estos archivos modificados (`git add`) y finalmente confirmas (`git commit`) todos los cambios preparados (`staged`).

<img src="https://i.imgur.com/FaLksEv.png">

## 3.1. Revisando el estado de tus archivos

El comando `git status` nos permite determinar en que estado se encuentran nuestros archivos.

+ Si ejecutaramos este comando inmediatamente después de clonar un repositorio:
```bash
$ git status
On branch master ## rama en que estamos. 'master' es la rama por defecto
nothing to commit, working directory clean ## no hay archivos rastreados y modificados
```

+ Supongamos que añadimos un nuevo archivo. Al ejecutar `git status` veríamos el archivo sin rastrear:
```bash
$ git status
On branch master
Untracked files:
...
```
+ `Sin rastrear` significa que Git ve archivos que no teníamos en el `commit` anterior.
+ Git no los incluirá en el próximo `commit` a menos que se le indique explicítamente (`git add`).
+ Si desearas incluirlo, debes comenzar a rastrearlo (`git add`).

## 3.2. Rastrear archivos nuevos

Para comenzar a rastrear un archivo: `git add`. 

+ Si queremos rastrear un archivo llamado `README`:
```bash
$ git add README
```

+ Al ver el estado del proyecto, el archivo `README` esta siendo **rastreado** y esta **preparado** para ser confirmado.


## 3.3. Ignorar archivos


---
## Añadiendo flags

Cuando se antepone `--` es porque a continuación viene una palabra.

--<palabra> 

Ejemplo:

// Cuando se pone un solo `-` significa que cada letra a continuación es un comando independiente.

-<letra><letra>... 

```bash
git status -s
git status -s -b // s: silent, b: branch
```


---


# 3. Configuración


Muestra la 
+ rama actual.
+ archivos en el stage.
+ archivos que no están en el stage.
```bash
git status
```

Agrego archivos para que este pendiente de sus cambios.
```bash
git add .
```
Sube los cambios al repositorio distribuido.
```bash
git commit -m "message"
```

# 4. Comandos útiles

## 4.1. git init

+ Inicia un repositorio local.
+ Crea una carpeta `.git` la cual contendrá el historial de todas las modificaciones que realicemos en el repositorio.

## 4.2. git status

+ Muestra cambios desde el último commit a la fecha.

Muestra:
+ Rama actual.
+ Archivos en el STAGE.
+ Archivos que no estan en el STAGE.
+ Cambios pendientes: ficheros que han recibido modificaciones desde el último commit.

## 4.3. git add 

+ Prepara cambios para enviarlos al repositorio: envía archivos al `STAGE`.
+ Existen diferentes formas. Lo ideal es que cada commit responda a algo específico.

```bash
git add .
git add -A
git add -u
git add *
git add -all
```

|   | Archivos nuevos | Archivos modificados | Archivos eliminados |
|-- |--|--|--|
| git add -A | - | - | - | 


https://stackoverflow.com/questions/26042390/git-add-asterisk-vs-git-add-period

```bash
git add . # git add -all // git add -A  // Agrega todos los archivos
git add *.png # Agrega todos los archivos .png del directorio actual
git add "*.png" # Agrega todos los archivos .png de todo el proyecto
git add index.html config.ts # Agrega un listado de archivos
git add pdfs/*.pdf # Agrega todos los archivos .pdf de la carpeta pdfs
git add pdfs/ # Agrega todos los archivos de la carpeta pdfs

git commit -m "agregando imagenes png"

git add css/
git commit -m "agrengando CSS"

# agregar todos y luego excluir uno
git add -A # igual a git add .??
git reset *.xml # excluye todos los archivos xml
```

## Crea registro histórico
Crea registro histórico con archivos en el stage.


## git checkout

Permite revertir cambios dejándo el proyecto según el último commit realizado.
```bash
git checkout -- .
git checkout -- <nombre_archivo>
```
## git log

Muestra el historial de cambios desde lo mas reciente a lo mas antiguo.

```bash
git log # todo el historial
git log --oneline # historial de forma resumida
git log --oneline --decorate --all --graph # decorate y graph permite mostrar arbol graficamente
git log -- <file_name>
git log --follow <file_name>
```
hash
HEAD: último commit en la rama actual
rama actual
Autor
fecha

```bash
git status -sb = git status -s -b
```

```bash
# comando visto en instagram:
# Usado cuando intento psuhear algo y me doi cuenta que ha habido cambios en el flujo principal
alias repush="git pull --rebase && git push"
alias repush="git push -f"


```

Para ver la lista de todos los alias añadidos a la configuración:
```
git config -- global -l
```
Si queremos ver y modificar:
```
git config -- global -e
```
## git diff

+ Muestra cambios entre el último commit y el momento actual.

Para verificar cambios si los archivos estan en `STAGE`.
```
git diff --staged
```

git diff a fondo

````md
diff --git a/README.md b/README.md
index af24015..57fc052 100644
--- a/README.md
+++ b/README.md
```diff
    @@ -227,7 +227,7 @@
    Muestra la
    + rama actual.
    + archivos en el stage.
    -+ archivos que no están en el stage ()
    ++ archivos que no están en el stage.
```
````
## Sacar archivos del STAGE

```
git reset HEAD <nombre_archivo>

```
## git commit 

Enviar archivos al `STAGE` y hacer push en un solo comando:
```
git commit -am <message>
```
Actualizar un commit:
```
git commit --amend -m <new_message>
```

## git reset

`HEAD^`: Apunta al penúltimo commit.
Deje en el penultimo commit sin eliminar los cambios. Deja los cambios fuera del STAGE.
```
git reset --soft HEAD^
git reset --soft <id_commit>^
```

`--mixed`: comando por defecto si no añadieramos un flag.
Nos movemos a un punto en el tiempo.
Archivos son quitados del stage pero aun contienen las modificaciones.
```
git reset --mixed <id_commit>
```

Nos movemos a un punto de la historia destruyendo todos los archivos que no corresponden a ese punto.
```
git reset --hard <id_commit>
```
## git reflog

+ Permite regresar a un punto a pesar de haber hecho un git reset.
+ Git siempre mantiene un registro de todo lo que sucede en el repositorio.

Aquí buscamos el id del punto al que queramos volver. Luego
```
git reset --hard <id_commit>
```

## Viajes en el tiempo


## Cambiar nombre de archivos

+ Git no rastrea explicitamente cambios de nombre en archivos. 
+ Si renombra un archivo, no se guardará ningún metadato que indique que renombró el archivo.

Al cambiar un nombre de archivo manualmente, por ejemplo a tráves de VSCode o usando el comando mv sucede lo siguiente:

<img src="https://i.imgur.com/f6YJYmx.png">

- ¿Cómo se detecta el cambio de nombre?

## git mv

```
git mv <file_name.ext> <new_file_name.ext>
```
+ Este comando permite ser explciito.
+ Equivale a la ejecución de lo siguiente:
```
mv <file_name.ext> <new_file_name.ext>
git rm <file_name.ext>
git add <new_file_name>
```
El comando mv equivale a cambiar el nombre de un archivo manualmente.

<img src="https://i.imgur.com/iE0Gcdo.png">

<img src="https://i.imgur.com/ZeZYHXD.png">

<img src="https://i.imgur.com/eu4Dcz9.png">

<img src="https://i.imgur.com/vArzTiy.png">
<br>
<img src="https://i.imgur.com/7owrOAz.png">

También es posible cambiar los nombres manualmente pero por Git es tomado como si se hubiese eliminado un archivo y creado otro con otro nombre.

La ventajas de git mv es que git llevará un control correcto de que hubo una modificación de nombre. De esta forma con el historico de cambios puedes ver como se llamaba anteriormente el archivo.

Ejercicio:
Cambiar el nombre de varios archivos a su equivalente en inglés.

## git rm

Eliminar archivo.

Para llevar el control de eliminación se debe usar

```
git rm <file_name.ext>
```

https://www.iteramos.com/pregunta/3962/cual-es-el-proposito-de-git-mv
https://github.com/mikeizbicki/ucr-cs100/blob/2015winter/textbook/cheatsheets/git-cheatsheet.md
https://try.github.io/
https://github.com/pcottle/learnGitBranching
https://datagoodie.com/blog/git-simple-tutorial-explanation-LEVEL-4/
https://learngitbranching.js.org/
<h1 align="center">Entendiendo Git</h1>

<img src="https://miro.medium.com/max/5000/0*a2jcqSzpTl6HQp35">

# Tabla de Contenido

- [1. Sobre el Control de Versiones](#)
    - [1.1. Instalación de Git](#)
    - [1.2. Configurando Git por primera vez](#)


# 1. Configurando Git por primera vez

Vamos a personalizar nuestro entorno y será necesario hacer estas cosas solo una vez. Puedes cambiar la configuración después ejecutando los comandos correspondientes.

`git config` permite obtener y establecer variables de configuración que controlan el aspecto y funcionamiento de Git.

Estas variables pueden almacenarse en 3 lugares:

1. `/etc/gitconfig`: contiene la configuración para todos los usuarios del sistema y todos sus repositorios. 
    - Si pasamos el flag `--system` a `git config`, lee y escribe en este archivo.
    ```bash
    git config --system -l ## ver los valores del archivo
    git config --system -e ## editar el archivo
    ```
2. `~/.gitconfig` o `~/.config/git/config`: configuración de tu usuario. 
    -  Si pasamos el flag `--global` a `git config`, lee y escribe en este archivo.
    ```bash
    git config --global -l ## ver los valores del archivo
    git config --global -e ## editar el archivo
    ```
3. `.git/config`: configuración del repositorio actual.

Cada nivel sobrescribe los valores del nivel anterior, por lo que los valores de `.git/config`[3] tienen preferencia sobre los de `/etc/gitconfig`[1].

## 1.1. Estableciendo nuestro editor

Por ejemplo, en el archivo de configuración `--system` esta establecido el editor que selecionamos durante la instalación de Git y esta configuración afecta a todos los usuarios del sistema. Podríamos establecer otro editor en la configuración `--global` para que afecte solo a nuestro usuario del sistema. En este caso estableceremos **VSCode** como editor:
```bash
git config --global core.editor code
```
## 1.2. Estableciendo alias para nuestros comandos

Podemos añadir alias a la configuración de git.
```bash
git config --global alias.l "log --oneline --decorate --all" # 'l' es el shortcut
git config --global alias.s "status -s -b"
```

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
+ archivos que no están en el stage ()
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
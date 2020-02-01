<h1>Entendiendo Git</h1>

# 1. Introducción
# 2. Instalación

## 2.1. Windows
## 2.2. Linux
## 2.3. Mac

# 3. Configuración


Muestra la 
+ rama actual.
+ archivos en el stage.
+ archivos que no están en el stage ()
```
git status
```

Agrego archivos para que este pendiente de sus cambios.
```
git add .
```
Sube los cambios al repositorio distribuido.
```
git commit -m "message"
```

# 4. Comandos útiles

## Iniciar repositorio local:

Suponiendo que ya tenemos un proyecto y estamos situados dentro del directorio de este.
```
git init
```
Este comando crea una carpeta .git la cual contiene un historial de todas las modificaciones que hemos realizado en nuestro repositorio.

## Ver cambios desde el último commit a la fecha:
```
git status
```
+ Rama actual.
+ Cambios pendientes. Ficheros que han recibido modificaciones desde el último commit.

## Preparar cambios para enviarlos al repositorio
```
git add 
```
+ Envía archivos al stage.

## Diferentes formas de enviar archivos al STAGE
Lo ideal es que cada commit responda a algo específico.
```
git add . // git add -all // git add -A  // Agrega todos los archivos
git add *.png // Agrega todos los archivos .png del directorio actual
git add "*.png" // Agrega todos los archivos .png de todo el proyecto
git add index.html config.ts // Agrega un listado de archivos
git add pdfs/*.pdf // Agrega todos los archivos .pdf de la carpeta pdfs
git add pdfs/ // Agrega todos los archivos de la carpeta pdfs

git commit -m "agregando imagenes png"

git add css/
git commit -m "agrengando CSS"

// agregar todos y luego excluir uno
git add -A // igual a git add .??
git reset *.xml // excluye todos los archivos xml
```

## Crea registro histórico
Crea registro histórico con archivos en el stage.


## Revertir cambios
Reconstruye el proyecto dejándolo como el último commit que realizamos.
```
git checkout -- .
git checkout -- <nombre_archivo>
```
## Ver historial de cambios
Ver cambios desde el más reciente a mas viejo.
```
git log // Ver todo el historial
git log --oneline // Ver historial de forma resumida
git log --oneline --decorate --all --graph // decorate y graph permite mostrar arbol graficamente

```
hash
HEAD: último commit en la rama actual
rama actual
Autor
fecha

## Agregando comandos

--<palabra> // Cuando se ponen dos "--" es porque a continuación viene una palabra
Ejemplo:
```
git status -s
git status -s -b // s: silent, b: branch
```

-<letra><letra>... // Cuando se pone un solo "-" significa que cada letra a continuación es un comando independiente

## Creando alias para nuestros comandos

Podemos añadir alías a la configuración de git.
```
git config --global alias.l "log --oneline --decorate --all" // 'lg' es el shortcut
git config --global alias.s "status -s -b"
```

```
git status -sb = git status -s -b
```

```
// comando visto en instagram:
// Usado cuando intento psuhear algo y me doi cuenta que ha habido cambios en el flujo principal
alias repush="git pull --rebase && git push"
alias repush="git push -f"


```

Para ver la lista de todos los alias añadidos a la configuración:
```
git config -- global -l
```
```
Si también queremos modificarla:
git config -- global -e
```
## Ver cambios

Visualizar cambios entre el último commit y el momento actual.
```
git diff
```

Verificar cambios si los archivos estan en STAGE.
```
git diff --staged
```
## Sacar archivos de STAGE

```
git reset HEAD <nombre_archivo>

```

## Enviar archivos al STAGE y hacer push en un solo comando

```
git commit -am <message>
```

## Actualizar un commit
```
git commit --amend -m <new_message>
```

## Git Reset

HEAD^: Apunta al commit anterior al último.
Deje en el penultimo commit sin eliminar los cambios. Deja los cambios fuera del STAGE.
```
git reset --soft HEAD^
git reset --soft <id_commit>^
```

mixed: comando por defecto si no añadieramos un flag.
Nos movemos a un punto en el tiempo.
Archivos son quitados del stage pero aun contienen las modificaciones.
```
git reset --mixed <id_commit>
```

Nos movemos a un punto de la historia destruyendo todos los archivos que no corresponden a ese punto.
```
git reset --hard <id_commit>
```

Regresar a un punto a pesar de haber hecho un git reset.
Git siempre mantiene un registro de todo lo que sucede en el repositorio.
```
git reflog
```

Aquí buscamos el id del punto al que queramos volver. Luego
```
git reset --hard <id_commit>
```

## Viajes en el tiempo


## Cambiar nombre de archivos

+ Git no rastrea explicitamente cambios de nombre en archivos. 
+ Si renombra un archivo, no se guardará ningún metadato que indique que renombró el archivo.

<img src="https://i.imgur.com/f6YJYmx.png">

- ¿Cómo se detecta el cambio de nombre?

### Git mv

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

<img src="https://i.imgur.com/iE0Gcdo.png">

<img src="https://i.imgur.com/ZeZYHXD.png">

<img src="https://i.imgur.com/eu4Dcz9.png">

<img src="https://i.imgur.com/vArzTiy.png">
<br>
<img src="https://i.imgur.com/7owrOAz.png">

También es posible cambiar los nombres manualmente pero por Git es tomado como si se hubiese eliminado un archivo y creado otro con otro nombre.

La ventajas de git mv es que git llevará un control correcto de que hubo una modificación de nombre. De esta forma con el historico de cambios puedes ver como se llamaba anteriormente el archivo.


## Eliminar archivo

Para llevar el control de eliminación se debe usar

```
git rm <file_name.ext>
```

https://www.iteramos.com/pregunta/3962/cual-es-el-proposito-de-git-mv

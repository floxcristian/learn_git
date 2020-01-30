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
git config --global alias.lg "log --oneline --decorate --all" // 'lg' es el shortcut
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
git reset HEAD <archivo>

```

## Enviar archivos al STAGE y hacer push en un solo comando

```
git push -am "message"
```

## Actualizar un commit
```
git commit --amend -m "new_message"
```

## Git Reset

```
git reset --soft HEAD
```


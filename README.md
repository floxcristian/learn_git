<h1 align="center">Entendiendo Git</h1>

<img src="https://miro.medium.com/max/5000/0*a2jcqSzpTl6HQp35">

## Tabla de Contenido

- [1. Sistemas de Control de Versiones](#)
- [2. Introducción a GIT](#)
- [3. Instalando GIT](#)
- [4. Configurando GIT](#)
- [5. Uso básico](#)
- [6. Ramas](#)



# 3. Guardando cambios en el repositorio

+ Vamos a realizar cambios y confirmar instantáneas `[snapshots]` de esos cambios en el repositorio cada vez que se alcance un estado que queramos conservar.

Cada archivo del repositorio puede tener 2 estados:
+ **tracked:** archivos que estaban en la última instantánea del proyecto. Pueden ser archivos sin modificar, modificados, o preparados (`staged`).
+ **untracked:** archivos en el `working directory` que no estaban en la última instantánea y no están en el `staging area`.

Ciclo de vida del estado de tus archivos:
+ Cuando clonas un repositorio todos los archivos estarán `tracked` y sin modificar. 
+ Mientras editas, Git los ve como modificados (han sido cambiados desde su último commit).
+ Luego preparas estos archivos modificados (`git add`) y finalmente confirmas (`git commit`) todos los cambios preparados (`staged`).

<img src="https://i.imgur.com/FaLksEv.png">

# 3. Estado de nuestros archivos

Cambios desde el último commit a la fecha:
<pre>
$ git status
</pre>

Cambios de forma compacta:
<pre>
$ git status --short
$ git status -s
</pre>

<pre>
$ git status -sb
$ git status -s -b #branch?
</pre>

Muestra:
+ Rama actual.
+ Archivos en el STAGE.
+ Archivos que no estan en el STAGE.
+ Cambios pendientes: ficheros que han recibido modificaciones desde el último commit.

+ Si ejecutaramos este comando inmediatamente después de clonar un repositorio:
<pre>
$ git status
<i>
On branch master ## rama en que estamos. 'master' es la rama por defecto
nothing to commit, working directory clean ## no hay archivos rastreados y modificados
</i>
</pre>

+ Supongamos que añadimos un nuevo archivo. Al ejecutar `git status` veríamos el archivo sin rastrear:
<pre>
$ git status
<i>On branch master
Untracked files:
...</i>
</pre>
+ `Sin rastrear` significa que Git ve archivos que no teníamos en el `commit` anterior.
+ Git no los incluirá en el próximo `commit` a menos que se le indique explicítamente (`git add`).
+ Si desearas incluirlo, debes comenzar a rastrearlo (`git add`).

> Al ver el estado del proyecto con `git status`, vemos que los archivos estan siendo **rastreados** y estan **preparados** para ser confirmados `changes to be commited`.

<pre>
  M  README
M M  Rakefile
A    lib/git.rb
M    lib/simplegit.rb
? ?  license.txt
</pre>

El estado aparece en 2 columnas.
<pre>
<b>izq:</b> preparado.
<b>der:</b> sin preparar.
</pre>
Los estados pueden ser:
<pre>
<b>??:</b> no rastreados.
<b>A:</b> preparados.
<b>M:</b> modificados.
</pre>

Ejemplo: 
+ `README` esta modificado en el `working directory` pero no está preparado.
+ `lib/simplegit.rb` esta modificado y preparado.
+ `Rakefile` esta modificado, preparado y modificado otra vez, por lo que hay cambios preparados y sin preparar.



---

## 3.2. Rastrear archivos nuevos / Añadir cambios al STAGING AREA

Prepara cambios para enviarlos al repositorio: envía archivos al `STAGING AREA`.

+ Rastrear un archivo específico:
<pre>
git add <b>README.md</b>
</pre>
+ Rastrear múltiples archivos:
<pre>
git add <b>index.html index.js</b>
</pre>
+ Rastrear todos los archivos:
<pre>
git add .
</pre> 

<pre>
git add -A
git add -u
git add *
git add -all
</pre>



---
## Añadiendo flags

Cuando se antepone `--` es porque a continuación viene una palabra.

--<palabra> 

Ejemplo:

// Cuando se pone un solo `-` significa que cada letra a continuación es un comando independiente.

-<letra><letra>... 



---

## 4.3. git add 


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



# 9. Historial de versiones

Historial de commits:
<pre>
git log
</pre>

Cada commit en una línea (salida más compacta):
<pre>
git log --oneline
</pre>

Historia en forma de grafo:
<pre>
git log --graph
</pre>


Muestra todos los commits creados, el lugar en el que estamos `HEAD` y la rama actual `master`.

```bash
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
# comando visto en instagram:
# Usado cuando intento psuhear algo y me doi cuenta que ha habido cambios en el flujo principal
alias repush="git pull --rebase && git push"
alias repush="git push -f"

```

## git diff

+ Muestra cambios entre el último commit y el momento actual.
+ Muestra todos los cambios que realizamos en relación a lo que esta en el master remoto.
+ Para salir presiono `q`.

```bash
git diff README.md
```


Para verificar cambios si los archivos estan en `STAGE`.
```
git diff --staged
```

git diff a fondo

```
- lineas eliminadas
+ lineas agregadas
diff --git a/README.md b/README.md
index af24015..57fc052 100644
--- a/README.md
+++ b/README.md
@@ -227,7 +227,7 @@
Muestra la
+ rama actual.
+ archivos en el stage.
-+ archivos que no están en el stage ()
++ archivos que no están en el stage.
```
## Sacar archivos del STAGE

```
git reset HEAD <nombre_archivo>


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


Muestra el historial de lo que hemos hecho localmente desde clonamos el repositorio.
Muestra clone, commits,
Esto es más preciso que hacer git log, porque esta traerá todos los commits, no solo los locales, si no también los de compañeros 
```bash
git reflog
```

Aquí buscamos el id del punto al que queramos volver. Luego
```
git reset --hard <id_commit>
```


# 11. Conectar repositorio local a servidor remoto:

<pre>
$ git remote add origin <b>https://github.com/floxcristian/learn_git</b>
</pre>


## git push

Despliega un login para ingresar a nuestra cuenta de Github y subir el código.
```bash
git push -u origin master
```

## git blame

Detalla cada línea de un archivo respecto a quién lo modifico y en que commit.

## git reset
Sería lo contrario a git add. 

Excluir un archivo de la lista de agregados.
```bash
git bash reset index.js
```


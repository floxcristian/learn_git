<h1 align="center">Uso básico de GIT</h1>

# 1. Inicializando un repositorio

<pre>
git init
</pre>

# 2. Clonando un repositorio

<pre>
git clone <b>https://github.com/floxcristian/learn_git</b>
</pre>


Crea una nueva carpeta con el nombre del repositorio y una subcarpeta oculta `.git`, descarga toda la información del repositorio y envía una copia de la última versión al `working directory`.

Clonar un repositorio en una carpeta específica:
<pre>
$ git clone <b>https://github.com/floxcristian/learn_git my_repo</b>
</pre>


# 7. Confirmar cambios

<pre>
$ git commit -m <b>"initial commit"</b>
</pre>

Confirmar cambios y hacer push en un solo comando:
<pre>
$ git commit -am <b>"new commit"</b>
</pre>

Actualizar el último commit (mensaje y cambios):
<pre>
$ git commit --amend -m <b>"my message"</b>
</pre>

+ No hay conflictos pero otro compañero ha hecho push antes:
<pre>
$ git pull
$ git commit -m "merge with latest changes"
$ git push
</pre>

+ Hay conflictos. El código a pushear entra en contradicción con el último commit.
<pre>
$ git pull
-- resolver conflictos visibles en el IDE
$ git add .
$ git commit -m "solved merge conflicts"
$ git push
</pre>


## 7.1. Referenciar un commit

+ Cada commit tiene un hash único de 40 carácteres hexadecimales.

+ Dos formas de referenciar:
  + **nombre absoluto:** primeros 4 dígitos del hash.
  + **nombre relativo:** `HEAD` último commit, `HEAD~1` penúltimo commit,  `HEAD~2` antepenúltimo commit, etc.



# 10.  Revertir cambios

Revertir cambios dejándo el proyecto o archivo específico según el último commit realizado.

<pre>
$ git checkout -- .
$ git checkout . #diferencias?
</pre>

Revertir cambios de un archivo específico:
<pre>
$ git checkout -- <b>README.md</b>
</pre>

Revertir cambios de un fichero a la versión correspondiente del commit:
<pre>
$ git checkout <b>98f0</b> -- <b>README.md</b>
</pre>

<pre>
$ git checkout <b>HEAD</b> -- <b>README.md</b>
</pre>

# 3. Cambiar nombre de archivos

+ Git no rastrea explicitamente cambios de nombre en archivos. 
+ Si renombra un archivo, no se guardará ningún metadato que indique que renombró el archivo.

Al cambiar un nombre de archivo manualmente, por ejemplo a tráves de VSCode o usando el comando mv sucede lo siguiente:

<img src="https://i.imgur.com/f6YJYmx.png">

- ¿Cómo se detecta el cambio de nombre?

# 4. Eliminar archivos

<pre>
$ git mv <file_name.ext> <new_file_name.ext>
</pre>

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

# 5. Eliminar archivos

Para llevar el control de eliminación se debe usar

<pre>
$ git rm <b>my_file.md</b>
</pre>

https://www.iteramos.com/pregunta/3962/cual-es-el-proposito-de-git-mv
https://github.com/mikeizbicki/ucr-cs100/blob/2015winter/textbook/cheatsheets/git-cheatsheet.md
https://try.github.io/
https://github.com/pcottle/learnGitBranching
https://datagoodie.com/blog/git-simple-tutorial-explanation-LEVEL-4/
https://learngitbranching.js.org/

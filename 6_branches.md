<h1 align="center">Trabajando con ramas</h1>

# 1. Gestionando nuestras ramas

Ver ramas existentes indicando con un * la rama activa:
<pre>
$ git branch
</pre>

Crear una rama:
<pre>
$ git branch <b>my_branch</b>
</pre>

Cambiar de rama:
<pre>
$ git checkout <b>my_branch</b>
</pre>

Crear una rama y activarla en un solo paso:
<pre>
$ git checkout -b <b>my_branch</b>
</pre>

Eliminar una rama:
<pre>
git branch -d <b>my_branch</b>
</pre>



# 2. Fusión de ramas

Siempre debemos estar en la rama master antes de fusionar las ramas.

Integrar cambios de una rama específica en la rama actual:
<pre>
$ git merge <b>experiment</b>
</pre>

## 2.1. Sin commits en el master 

La otra rama solo se une a master sin mayor conflicto.
No tenemos nada en el master antes de hacer el merge.
Fast-forward

<img src="https://i.imgur.com/t73Sf5F.png">

El commit solo se paso a master y se puso al final.

<img src="https://i.imgur.com/nU2bp0K.png">

## 2.2. Teniendo commits en el master

<img src="https://i.imgur.com/wGTNMq5.png">


Al intentar hacer merge de las ramas nos aparecerá el editor en donde debemos indicar el nombre que le daremos al commit que unirá las ramas.
Por defecto el nombre será Merge branch ***my_branch**

Luego de fusionar las ramas debemos eliminar la rama que ya fusionamos:
<pre>
$ git branch -d <b>experiment</b>
</pre>

# Resolución de conflictos

Si en dos ramas modificamos el mismo archivo, al hacer merge git no sabrá con cual de las opciones quedarse.
<pre>
$ git merge <b>testBranch</b>
<i>
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
</i>
</pre>
Si desde VSCode vamos al archivo que genera conflictos, veremos que nos mostrará los dos cambios que generan conflictos. Aquí podemos seleccionar las opciones que nos muestra VSCode:
<pre>
+ Aceptar cambio actual
+ Aceptar cambio entrante
+ Comparar cambios
</pre>

 

Aquí deberemos seleccionar una opción o eliminar las líneas 
<pre>

 <<<<<<<< HEAD

 ======

 >>>>>>>>>>>>
 </pre>

 Una vez resuelto el conflicto debemos añadir los cambios:
<pre>
$ git add .
</pre>

confirmar los cambios:
<pre>
$ git commit -m <b>"new commit"</b>
</pre>

y subirlos al repositorio remoto:
<pre>
$ git push
</pre>


fast-forward
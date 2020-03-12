<h1 align="center">Trabajando con ramas</h1>

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



Fusión de ramas

Integrar cambios de una rama específica en la rama actual:
<pre>
$ git merge <b>experiment</b>
</pre>

## Resolución de conflictos

Si en dos ramas modificamos el mismo archivo, al hacer merge, git no sabrá con cual de las opciones quedarse.
<pre>
$ git merge <b>testBranch</b>
<i>
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
</i>
</pre>
 Veremos que en VSCode nos mostrará los dos cambios que generan conflictos 
 
 <<<<<<<< HEAD

 ======

 >>>>>>>>>>>>

 Aquí podemos seleccionar las opciones que nos muestra VSCode. 
 Aceptar cambio actual
 Aceptar cambio entrante
 Comparar cambios

 Una vez resuelto el conflicto debemos añadir al stage
 git add .
 y hacemos el commit
 git commit


fast-forward
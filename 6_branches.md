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

Resolución de conflictos



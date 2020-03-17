# 7. Confirmar cambios

Establecer mensaje a tráves del editor:
<pre>
$ git commit
</pre>

Añadir diff a descripción de la confirmación:
<pre>
$ git commit -v
</pre>

Escribir mensaje de confirmación directamente:
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



## 7.1. Referenciar un commit

+ Cada commit tiene un hash único de 40 carácteres hexadecimales.

+ Dos formas de referenciar:
  + **nombre absoluto:** primeros 4 dígitos del hash.
  + **nombre relativo:** `HEAD` último commit, `HEAD~1` penúltimo commit,  `HEAD~2` antepenúltimo commit, etc.

# Casos de Ejemplo


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

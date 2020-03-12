git diff
compara lo que tengo en el ultimo commit con lo que tengo actualmete (fuera del stage)

cuando crear commits
-implemetación de un feature
refactorizacion
instalacion de componentes

...cuando tengamos algo facil de describir..

---

<h1 align="center">Caso Práctico</h1>

Cuando me equivoco en un commit no es recomendable crear otro que corrija ese error.
Lo recomendable es corregir ese commit o si 2 commits hacen lo mismo se podrian fusionar? 

para ello volvemos al commit base con
git reset --soft 09fb

esto regresa al commit indicado y los cambios los deja en stage 

Si hago git diff no parecera nada porque los cambios estan en stage
para ver los cambios entre el ultimo cmmit y lo que esta en stage ejecuto
git diff --staged

Para actualizar el ultimo commit (mensaje y cambios)
git commit --amend -m "nuevo mensaje"

Con esto agregamos cambios que no queremos poner en un commit nuevo

---

Compartir proyectos para contribuir en el desarrollo

Vamos a registrar un sevidor remoto como github o gitbucket

también podemos levantar nuestro propio servidor de git con gitlab

voy a añadir un servidor remoto por medio de origin que se encontrará en la dirección x
<pre>
git remote add origin https:....
</pre>


empujamos nuestro codigo au n servidor remoto, en este caso github
con -u no me va a estar preguntando todo el timepo en que rama hare mis push, siempre usará los comandos sigueintes, uso el servidor origin que se encuentra en github y la rama master
git push -u origin master
permite depsues usar el comando git push sin especificar el resto


obttener cambios de github
git pull


verificar remotos
git remote -v

eliminar un remoto
git remote rm origin


--- 
integrar cambios de una rama a otra

git merge my_branch

fast forward: 


--decorate: muestra las referencias de cada commit

Eliminar una rama (despues de fusionarla con master);

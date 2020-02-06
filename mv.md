# Cambiar nombre de archivos

```
git mv oldname newname
```

es la abreviatura de:

```
mv oldname newname
git add newname
git rm oldname
```
Git intenta adivinar lo que desea hacer. Realiza cada intento de preservar la historia ininterrumpida.
Por supuesto, no es perfecta.

Git mv permite ser explicito con su intención y evitar así algunos errores.

---
## Ejemplo 1:

```
mv a c
mv b a
git status
```
Resultado:
```
# modified: a 
# deleted: b

# Untracked files:
c
```

Si quisieramos ver el historial de lo que se hizo mas adelante veríamos algo como lo siguiente:
```
git diff
```

--- 
# Ejemplo 2:

Mover el archivo hello.html a la carpeta lib.

```
mkdir lib
git mv hello.html lib
git status
```
Resultado:
```
renamed:    hello.html -> lib/hello.html
```
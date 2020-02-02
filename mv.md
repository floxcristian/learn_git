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
Ejemplo 1:

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
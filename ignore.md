<h1 align="center">Ignorar archivos</h1>

Archivos que no queremos que GIT añada automáticamente ni tampoco aparezcan como `no rastreados`.

+ creados automáticamente.
+ creados por el sistema de compilación.

# 1. Lista de patrones
Ignora archivos que terminan con `o` o `a`:
```
*.[oa] 
```
Ignora archivos que terminan en `~`, lo cual es usado por varios editores para marcar archivos temporales:
```
*~
```
# 2. Reglas sobre patrones
- ignorar líneas en blanco y que comiencen con `#`.
- pueden terminar en `/` para especificar un directorio.
- pueden negarse si al principio se añade `!`.
- aceptan patrones glob.

## 2.1. Patrones glob

Especie de expresión regular usada por terminales.
```
(*): 0 o más carácteres.
[abc]: cualquier carácter dentro de los corchetes (a, b o c).
(?): carácter cualquiera.
[0-9]: carácter entre 0 y 9.
**: directorios anidados.
```

La expresión `a/**/z` permite valores como:
```
a/z
a/b/z
a/b/c/z
```
# 3. Ejemplos

```bash
*.a # ignora archivos terminados en .a
!lib.a # excepto lib.a
/build # ignora todos los archivos del directorio build/
doc/*.txt # ignora doc/notes.txt pero no doc/server/arch.txt
```

Github mantiene una extensa lista de archivos `.gitnore` adecuados a docenas de proyectos y lenguajes.
Puede encontrarlos en github/gitnore.



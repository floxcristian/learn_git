
<h1 align="center">Ver cambios específicos</h1>


Muestra los cambios (líneas añadidas y eliminadas) entre el último commit y lo no que hemos preparado:
<pre>
$ git diff
</pre>

Compara lo que esta en el último commit con lo que está en el `STAGE`:
<pre>
$ git diff --staged
$ git diff --cached
</pre>

# 1. Detalles de los cambios
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

# 2. Usando una herramienta externa

Ver cambios con un programa/interfaz:
<pre>
$ git difftool
</pre>

Ver que programas tenemos disponibles:
<pre>
$ git difftool --tool-help
</pre>
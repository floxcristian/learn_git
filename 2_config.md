<h1 align="center">2. Configurando GIT</h1>

`git config` permite obtener y establecer variables de configuración que controlan el aspecto y funcionamiento de Git.

Estas variables pueden almacenarse en 3 lugares:

1. `/etc/gitconfig`: archivo de configuración de todos los usuarios del sistema. 
    - Usamos `git config --system` para leer o modificar este archivo:
    ```bash
    git config --system -l ## ver los valores del archivo (-l: --list)
    git config --system -e ## editar el archivo (-e: --?)
    ```
2. `~/.gitconfig` o `~/.config/git/config`: archivo de configuración del usuario actual del sistema. 
    -  Usamos `git config --global` para leer o modificar este archivo:
    ```bash
    git config --global -l ## ver los valores del archivo
    git config --global -e ## editar el archivo
    ```
3. `.git/config`: archivo de configuración del repositorio actual.

Cada nivel sobrescribe los valores del nivel anterior, por lo que los valores de `.git/config[3]` tienen preferencia sobre los de `/etc/gitconfig[1]`.

# 1. Estableciendo nuestro editor

Por ejemplo, en el archivo de configuración `--system` está establecido el editor que selecionamos durante la instalación de Git y esta configuración afecta a todos los usuarios del sistema. Podríamos establecer otro editor en la configuración `--global` para que afecte solo a nuestro usuario de sistema. En este caso estableceremos **VSCode** como editor:
<pre>
git config --global core.editor <b>code</b>
</pre>
# 2. Estableciendo nuestra identidad

<pre>
$ git config --global user.name <b>"Cristian Flores"</b>
$ git config --global user.email <b>cristianflores.ee@gmail.com</b>
</pre>

Sobrescribir información en proyectos específicos:
<pre>
$ git config user.name <b>"Andrés"</b>
</pre>

## Activando coloreado de la salida??
<pre>
git config --global color.ui auto
</pre>

## Mostrar estado original en los conflictos??
<pre>
git config --global merge.conflictstyle diff3
</pre>

# 3. Estableciendo alias para nuestros comandos

<pre>
$ git config --global <b>alias.l</b> "log --oneline --decorate --all"
$ git config --global <b>alias.s</b> "status -s -b"
</pre>

Ver lista de todos los alias añadidos:
```
git config -- global -l
```
Modificar:
```
git config -- global -e
```

# 4. Comprobando nuestra configuración

Mostrar todas las propiedades que Git ha configurado:

<pre>
<b>$ git config --list</b>
<i>user.name=Cristian Flores
user.email=cristianflores.ee@gmail.com
color.status=auto
color.branch=auto
color.interactive=auto
color.diff=auto
...</i>
</pre>

Puede que veamos claves repetidas porque Git lee la misma clave de distintos archivos (por ejemplo, `/etc/gitconfig` y `~/.gitconfig`). En estos casos, Git usa el último valor para cada clave única que ve.

Comprobar el valor que Git utilizará en una clave específica:
<pre>
$ git config <b>user.name</b>
<i>Cristian Flores</i>
</pre>

# 5. Obteniendo ayuda

<pre>
git help
</pre>

Obtener ayuda de un comando específico:
<pre>
$ git help <b>commit</b>
$ git <b>commit</b> --help
$ man git-<b>commit</b>
</pre>

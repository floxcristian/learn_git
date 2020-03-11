<h1 align="center">Introducción a GIT</h1>

# 1. Los 3 estados

Estados en los que se pueden encontrar los archivos:
1. **commited:** almacenado de manera segura en nuestra db local.
2. **modified:** modificado pero todavía no confirmado a nuestra db local.
3. **staged:** marcado para que se vaya en el próximo commit.

Secciones de un proyecto Git:
1. **git directory (.git):** almacena metadatos y db para nuestro proyecto. Es lo que se copia cuando clonamos un repositorio.
2. **working directory:** copia de una versión del proyecto. Esta se saca de la db comprimida en el `git directory`, y se coloca en disco para poder usarla.
3. **staging area:** archivo en tu `git directory`, que almacena info de lo que irá en nuestro próximo commit.

# 2. Flujo de trabajo básico

1. Modificas archivos en tu `working directory`.
2. Preparas los archivos añadiendolos al `staging area`.
3. Confirmas los cambios, lo que toma los archivos tal como están en el `staging area` y los almacena de manera permanente en tu `git directory`.

<img src="https://i.imgur.com/7i9c2UK.png">

Adicionalmente:
+ Si una versión concreta de un archivo está en el `git directory` se considera `commited`.
+ Si se ha modificado desde que se obtuvo del repo, pero ha sido añadida al `staging area`, está `staged`.
+ Si se ha modificado desde que se obtuvo del repo, pero no se ha añadido al `staging area`, está  `modified`.

---

Git utiliza una arquitectura de 3 niveles:
1. **commit:** contiene información sobre el autor, momento y el mensaje de los cambios.
2. **tree:** cada commit contiene un árbol donde se registran los nombres y rutas de los archivos cuando se hizo el commit.
3. **blob:** para cada archivo del árbol hay un blob, que contiene la snapshot comprimida del archivo cuando se hizo el commit.

<<<<<<< HEAD:2_introduction.md
<img src="https://i.imgur.com/KosGd4Q.png">

Flujo de trabajo

Crea un archivo README (sin seguimiento)
Agrega el archivo al stagign area (empieza a dar seguimiento)
Realizar commit (registrar cambios

git init
echo "hola mundo" >> README.txt
git status
git add README.md
git status
git commit -m
git status
code README.md
touch LICENSE.md
git status
git add .
git status

git log
=======
<img src="https://i.imgur.com/KosGd4Q.png">
>>>>>>> 60b94e8bfa92a79b9c01f7bb014ddf43cd12bfca:introduction.md

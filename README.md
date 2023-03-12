# Guía de comandos de Git y Github

## Comandos

### Notas

Cosas de la terminal usualmente "--" indica una palabra completa, mientras que "-" indica una abreviatura.

### Comandos básicos

Propociona la versión actual de git que está instalada en la computadora:

```git
git --version
```

Proporciona una vista general de los comandos de git (git help):

```git
git help commit
```

Inicializar el repositorio:

```git
git init
```

Añadir archivos al stage, (para añadir todos se utiliza el "."), en el caso de querer añadri algo especifico
se pone el nombre del archivo: 

```git
git add .
```

Ver el estado actual de la rama:

```git
git status
```

### Config commando

Sirve para configurar el uso de git.

Configurar el nombre de usuario:

```git
git config --global user.name "Angel"
```

Configurar el correo: 

```git
git config --global user.email "ejemplo@gmail.com"
```

Ver el usuario de Git:

```git
git config --global -e
```

Fijar el nombre de la rama principal a main para todos los proyectos (configuración recomendada):

```git
git config --global init.defaultBranch main
```

### Commit comando

El commit sirve para guardar el repositorio de la manera en que se encuentra en el momento en el que se hace el commit.
Se puede definir como una especie de fotografía del proyecto en ese preciso momento.

Hacer un commit con un mensaje:

```git
git commit -m "Primer commit"
```

Hacer un commit y a la vez añadir añadir los archivos al stage:

```git
git commit -am "Commit con agregada de archivos"
```

Corregir un mensaje del último commit:

```
git commit --amend -m "instalaciones actualizadas"
```

### Branch 

Mostrar las ramas y la rama actual:

```git
git branch
```

Renombrar una rama, ejemplo para renombrar la rama master a main:

```git
git branch -m master main
```

Eliminar una rama: 

```
git branch -d rama-a-eliminar
```

Eliminar una rama aunque no se haya mezclado: 

```
git branch -d rama-a-eliminar -f
```

Ver Ramas y remotos:

```
git branch -a
```

### Checkout

Reconstruir el proyecto a como estaba en el commit anterior:

```git
git checkout -- .
```

Cambiar de una rama a otra:

```
git checkout otra-rama
```

Crear una rama y cambiarse a ella automaticamente:

```
git checkout -b rama
```

Regresar un archivo a como estaba en un commit especifico:

```
git checkout 6cd854b miembros.md
```

### Merge

Mezclar una rama con otra (Debes estar posicionado en la rama en la que quieres los cambios):

```
git merge rama-que-tiene-los-cambios
```

### Log

Logs del repositorio (mensajes y otras cosas)

Ver commits del repositorio:

```git
git log
```

Ver un log resumudo:

```
git log --oneline
```

### Stash

Mete los cambios al stash (un baúl para cambios):

```
git stash
```

Mostrar el stash (cambios):

```
git stash list
```

Traer los cambios del stash y borra el stash:

```
git stash pop
```

Borrar todo el stash:

```
git stash clear
```

Traer un stash especifico

```
git stash apply stash@{2}
```

Borrar un stash especifico:

```
git stash drop stash@{2}
```

Ver datos de un stash especifico:

```
git stash show stash@{2}
```

Agregar al stash con un nombre:

```
git stash save "nombre que desees"
```

### Reset 

Quitar del stage algún archivo, el siguiente ejemplo quita del stage el archivo.js:

```git
git reset archivo.js
```

Viajar a algún commit especifico, funciona tanto con el hash largo como con el corto, el --soft
es para mantener los cambios:

```
git reset --soft eecbcda
```

Viajar a algún commit especifico, funciona tanto con el hash largo como con el corto, el --mixed
quitar los cambios del estage de esa versión (es el que se hace por defecto cuando no se especifica):

```
git reset --mixed eecbcda
```

Viajar a algún commit especifico, funciona tanto con el hash largo como con el corto, el --hard
borra todo lo que estaba trackeado:

```
git reset --hard eecbcda
```

IR a algún commit el HEAD es el commit y el ^ indica el número de commit en el que estás retrocediendo por defecto uno
pero pueden ser más por ejemplo HEAD^2,HEAD^16, etc.

```
git reset --hard HEAD^
```

### Diff

Muestra las diferencias entre archivos:

```
git diff
```

Muestra las diferencias entre archivos del stage:

```
git diff --staged
```

### Rebase

El rebase ocupado de la siguiente forma trae todos los cambios que estan en el master (que no están en la rama),
y posteriormente añade los cambios de la rama, esto lo hace en la rama en la que te encuentras, si después hicieramos un merge de los cambios sería un fast-fordward.

```
git rebase master
```

Rebase interactivo con los últimos 4 commits para salir es ( :wq! , para activar el modo de comandos pulsa esc), para añadir presionar letra 'a' (append):

```
git rebase -i HEAD~4
```

#### Comandos del rebase interactivo

s: squash (fusionar el commit anterior con el que tiene la s)
r: reword cambiar el nombre del commit

### Reflog

Mostrar un historial de los cambios que se han hecho (útil para volver a una versión después de un reset): 

```
git reflog
```

### Mv

Renombrar un archivo (realmente es mover un archivo pero de paso se renombra en el ejemplo ya que se deja en
la carpeta solo cambiando el nombre):

```
git mv .\destruir-mundo.md salvar-mundo.md
```

### Rm

Eliminar un archivo pero lo deja en el stage, para eliminarlo completamente hacer el "commit -m": 

```
git rm .\salvar-mundo.md
```

### Tag

Crea un tag:

```
git tag nombre-tag
```

Mostrar tags: 

```
git tag
```

Borrar un tag:

```
git tag -d nombre-tag
```

Crear un tag con versionamiento anotated: 

```
git tag -a v1.0.0 -m "Version 1.0.0"
```

Crear un tag en un commit especifico (por si el tag lo quieres en algún commit anterior):

```
git tag -a v0.1.0 bdb7f35 -m "Version alpha de la app"
```

### Show

Mostrar información de un tag:

```
git show v1.0.0
```

## Archivos especiales

### .gitkeep

Es un archivo especial para cuando tengas una carpeta que no tenga ningún archivo y que quieras que se suba al stage.

### .gitignore

Archivo en el que podemos especificar a que carpetas y archivos no queremos darle seguimiento

## Crear comandos personalizados

para crear un comando se ejecuta el código siguiente donde ".s" es el nombre alias del comando que se llamaría "git s",
y el resto es el comando al cual hace referencia:

```
git config --global alias.s "status --short"
```

## Github


Comandos para un repositorio que ya ha sido creada y solo se quiere subir a github:

```
git remote add origin https://github.com/angelxescomx08/liga-justicia.git
git branch -M main
git push -u origin main
```

Subir todos los tags a github

```
git push --tags
```

### remote

Ver el origin que se tiene:

```
git remote -v
```

### pull

Traer los cambios de un repositorio, el comando es similar a (git pull origin main):

```
git pull
```

Traer todo con el git pull:

```
git pull --all
```

### clone

Clonar un repositorio:

```
git clone https://github.com/angelxescomx08/liga-justicia.git
```

### push

Subir los cambios a github:

```
git push
```

Subir una rama a github, si no te quieres aprender el comando usa primero el "git push" esto tirara un error
pero te escribirá que uses este comando:

```
git push --set-upstream origin rama-villanos
```

### fetch

El comando "git fetch" descarga todos los cambios y actualizaciones realizados en un repositorio remoto a tu repositorio local, pero no los fusiona automáticamente con tu código local. Esto permite revisar los cambios antes de mezclarlos en tu rama local. (Puedes usarlo antes de hacer un git pull)

```
git fetch
```

### remote

El "remote" en Git es una referencia a un repositorio en otro lugar, ya sea en el mismo sistema local o en un sistema remoto. En el contexto de GitHub, un "remote" es una referencia a un repositorio alojado en GitHub.

Añadir un repositorio remoto, el upstream es el nombre que se le da por convención cuando hacemos un fork,
el origin es cuando es uno de nuestros repositorios.

```
git remote add origin https://github.com/Klerith/legion-del-mal.git
```

```
git remote add upstream https://github.com/Klerith/legion-del-mal.git
```

Ver los repositorios remotos que tenemos:

```
git remote -v
```

Traer los cambios del upstream a una rama en este caso la master:

```
git pull upstream master
```

Remover los remotos de las ramas que han sido borradas y puseadas en github:

```
git remote prune origin
```

## Algunos conceptos

### Squash

Mezclar varios commits en uno solo.

### Fork

Un "fork" en GitHub se refiere a hacer una copia de un repositorio de código de otra persona en tu propia cuenta de GitHub.

### pull request

Es para generar todo el proceso de unión a un repositorio.

### Pasos para traer una rama de un compañero

1. Traer todos los cambios
2. mostrar las ramas y remotos (solo para ver que si se trajeron los cambios)
3. moverse a la nueva rama

```
git pull --all

git branch -a 

git checkout rama
```

### Milestone

Es una agrupador de labels, le puedes poner fecha para recordar que debes solucionar los issues antes de una fecha especifica

## Pasos para crear un repositorio y subirlo a github

1. inicializar repositorio
2. añadir los archivos al stage
3. hacer el commit
4. añadir el remoto origin que apunta a nuestro repositorio de github
5. hacer el push del al origin de la rama main (el -u es para que no tengamos que poner el origin después)

```
git init

git add .

git commit -m "primer commit"

git remote add origin https://github.com/angelxescomx08/avengers-github.git

git push -u origin main
```

## Pasos para borrar una rama y su remoto

1. Ver todas las ramas y sus remotos
2. Borrar la rama (Debería ya haberse subido a github)
3. Limpiar los remotos de las ramas borradas

```
git branch -a

git branch -d rama-a-borrar

git remote prune origin
```
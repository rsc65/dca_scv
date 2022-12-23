# DESARROLLO COLABORATIVO DE APLICACIONES
## AUTOR: SABATER CARBONELL, RAFAEL

---
## Código fuente utilizado para la práctica
El código empleado se ha creado en el momento de la práctica.
Consiste en un pequeño código fuente de `Python` que muestra mensajes por pantalla. 

---
## Ejecución
Con una nueva pestaña de terminal abierta en el directorio raíz, debemos ejecutar:
```shell
$ python dca.py
```

---
## Repositorio del proyecto
El repositorio empleado para este proyecto lo podemos encontrar en el siguiente enlace: [github.com/rsc65/dca_scv](https://github.com/rsc65/dca_scv).

Para importarlo de forma local y trabajar sobre él en nuestro ordenador, tan solo hemos tenido que situarnos en el directorio que deseemos que lo contenga, abrir una nueva pestaña de terminal y ejecutar la siguiente orden, teniendo `Git` instalado en el sistema:
```shell
$ git clone https://github.com/rsc65/dca_scv.git
```

---
## Alias
Hemos añadido alias a la configuración del repositorio local de `Git`, y también alguno a la configuración global de `Git`. 
Estos alias solo funcionarán en la máquina donde se han ejecutado.

Los alias sirven para acortar los comandos que utilizamos por consola.
Por ejemplo, un comando que se suele utilizar a menudo es `git pull`. 
Si lo quisiésemos acortar, pordríamos definir un alias para poner `git pl` y realice las mismas acciones.

### Alias locales
Estos alias solo funcionarán en la copia local de este repositorio en la máquina que se han creado.
Hemos añadido los siguientes:
```text
b = branch
ba = branch --all
co = commit
com = commit -m
pl = pull
ps = push
```
Para añadirlos, hemos ejecutado los siguientes comandos:
```shell
$ git config alias.b branch
$ git config alias.ba 'branch --all'
$ git config alias.co commit
$ git config alias.com 'commit -m'
$ git config alias.pl pull
$ git config alias.ps push
```

### Alias globales
Estos alias solo funcionarán en la máquina que se han creado, para cualquier proyecto de `Git`.
Hemos añadido los siguientes:
```text
a = add
all = add .
bsb = bisect bad
bsg = bisect good
bsr = bisect reset
bss = bisect start
sh = stash
shp = stash pop
```
Para añadirlos, hemos ejecutado los siguientes comandos:
```shell
$ git config --global alias.a add
$ git config --global alias.all 'add .'
$ git config --global alias.bsb 'bisect bad'
$ git config --global alias.bsg 'bisect good'
$ git config --global alias.bsr 'bisect reset'
$ git config --global alias.bss 'bisect start'
$ git config --global alias.sh stash
$ git config --global alias.shp 'stash pop'
```

## Fallo detectado en la aplicación
Al ejecutar la aplicación desde el commit [4c28af60d042ad7217a885512e34ba16d175f3ab](https://github.com/rsc65/dca_scv/commit/4c28af60d042ad7217a885512e34ba16d175f3ab), hemos detectado que hay un fallo.

La salida que nos muestra el programa es la siguiente:
```text
Desarrollo Colaborativo de Aplicaciones
Curso 2022/2023
Ingeniería Informática
Ingeniería del Software
Universidad de Alicante
Escuela Politécnica Superior

```
Cuando debería ser la siguiente:
```text
Desarrollo Colaborativo de Aplicaciones
Curso 2022/2023
Ingeniería Informática
Ingeniería del Software
Universidad de Alicante
Escuela Politécnica Superior
```
Es decir, hay un salto de línea de más.

No sabemos cuándo se ha producido este error, por lo que emplearemos `Git Bisect` para encontrarlo.
Para ello, seguiremos los siguientes pasos:

### Marcar un commit como erróneo
El commit especificado es erróneo, que además es el último que tiene en curso la copia local del repositorio.

Ejecutamos en la terminal:
```shell
$ git bss   # alias definido para 'bisect start'
$ git bsb   # alias definido para 'bisect bad'
```
La salida obtenida tras ejecutar ambas órdenes es la siguiente:
```text
status: waiting for both good and bad commits
status: waiting for good commit(s), bad commit known
```

### Marcar un commit como correcto
Sabemos que la aplicación funcionaba correctamente en el commit [dc419ecc6e60710ed68283cba9110b48538a8a03](https://github.com/rsc65/dca_scv/commit/dc419ecc6e60710ed68283cba9110b48538a8a03).

Ejecutamos en la terminal:
```shell
$ git bsg dc419ecc6e60710ed68283cba9110b48538a8a03  # alias definido para 'bisect good'
```
La salida obtenida tras ejecutar la orden es la siguiente:
```text
Bisecting: 2 revisions left to test after this (roughly 1 step)
[7ed0a675c1a051c7010756519a4e1cb4716b6b63] Alias creados. Commit creado empleándolos.
```
Y ya no nos encontramos sobre la rama `main`, sino que estamos en `(no branch, bisect started on main)`.

### Continuando con la búsqueda
Al ejecutar el programa en el punto que nos ha dejado `Git Bisect`, la salida es la siguiente:
```text
Desarrollo Colaborativo de Aplicaciones
Curso 2022/2023
Universidad de Alicante
```
Como es correcta, lo marcamos como correcto:
```shell
$ git bsg
```
La salida obtenida:
```text
Bisecting: 0 revisions left to test after this (roughly 1 step)
[9fccf151b8a84be76da9628d8369fdb2ec68bf2b] Grado añadido al código fuente.
```
Volvemos a ejecutar y obtenemos la siguiente salida:
```text
Desarrollo Colaborativo de Aplicaciones
Curso 2022/2023
Ingeniería Informática
Universidad de Alicante
Escuela Politécnica Superior

```
La salida es errónea, por lo que lo marcamos como erróneo.
```shell
$ git bsb
```
La salida obtenida:
```text
Bisecting: 0 revisions left to test after this (roughly 0 steps)
[af78454f37a334072d8ecf4939baead4a822579e] Escuela añadida al código fuente.
```
Volvemos a ejecutar y obtenemos la siguiente salida:
```text
Desarrollo Colaborativo de Aplicaciones
Curso 2022/2023
Universidad de Alicante
Escuela Politécnica Superior

```
La salida es errónea, por lo que lo marcamos como erróneo.
```shell
$ git bsb
```
La salida obtenida:
```text
af78454f37a334072d8ecf4939baead4a822579e is the first bad commit
commit af78454f37a334072d8ecf4939baead4a822579e
Author: Rafael Sabater Carbonell <rsc65@alu.ua.es>
Date:   Thu Dec 22 16:19:27 2022 +0100

    Escuela añadida al código fuente.

 dca.py | 1 +
 1 file changed, 1 insertion(+)
```

### Finalizando la operación
Hemos encontrado el commit en el que se introdujo el error, que es [af78454f37a334072d8ecf4939baead4a822579e](https://github.com/rsc65/dca_scv/commit/af78454f37a334072d8ecf4939baead4a822579e).

Ahora, vamos a finalizar la operación de `Git Bisect`:
```shell
$ git bsr   # alias para 'bisect reset'
```
La salida obtenida:
```text
Previous HEAD position was af78454 Escuela añadida al código fuente.
Switched to branch 'main'
Your branch is up to date with 'origin/main'.
```
Solo nos falta corregir el error y subir los cambios.

---
## Hooks
Los `Hooks` de `Git` son guiones que se ejecutan automáticamente antes o después de ejecutar acciones de `Git`.

Estos los podemos encontrar en el directorio `./.git/hooks`.
Inicialmente tenemos trece ejemplos, y si quisiésemos probar alguno, tendríamos que quitar la extensión `.sample` y darles permiso de ejecución (que, por defecto, estas muestras lo incluyen).

### Hook de `pre-commit`
Este `Hook` se ejecutará antes de cada commit.

Hemos creado una automatización que siempre añadirá el fichero `.gitignore` a cada commit nuevo que hagamos, si este ha cambiado.

El fichero `pre-commit` ha quedado del siguiente modo: 
```shell
#!/bin/sh
git add .gitignore
```
Ahora, vamos a modificar el `.gitignore` añadiendo los ficheos `.DS_Store` que genera automáticamente macOS al acceder a un directorio con el Finder.
Haremos commit únicamente del `README` y se añadirá también el fichero `.gitignore`.
Comenzamos haciendo `git status` para ver el contenido modificado:
```shell
$ git status
```
La salida obtenida:
```text
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   .gitignore
	modified:   README.md
```
Añadimos el fichero `README.md`:
```shell
$ git add README.md
$ git status
```
La salida obtenida:
```text
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   README.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   .gitignore
```
Hacemos el commit de este fichero y comprobamos que también se ha incluido el fichero `.gitignore`:
```shell
$ git commit -m "README actualizado con el apartado de Hooks. Aún sin finalizar."
$ git status
```
La salida obtenida:
```text
[main 3beb4b7] README actualizado con el apartado de Hooks. Aún sin finalizar.
 2 files changed, 93 insertions(+), 1 deletion(-)

On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

### Hook de `commit-msg`
Este `Hook` se ejecutará al intentar realizar un commit con un mensaje.

En esta ocasión, vamos a comprobar que el mensaje no sea vacío.
En este caso, emitiríamos un mensaje de error.

La diferencia en este `Hook` respecto al anterior es que, en lugar de emplear un script de `shell`, hemos creado uno de `Python`.
El script ha quedado del siguiente modo:
```Python
#!/usr/bin/env python3
import sys
with open(sys.argv[1], 'r') as f:
	if (f.read() == ""):
		print("ERROR. El mensaje del commit no puede ser vacío.")
		sys.exit(1)
```
Ahora, vamos a intentar hacer un commit del fichero `README.md` con un mensaje vacío:
```shell
$ git add README.md
$ git commit -m ""
```
La salida producida:
```text
ERROR. El mensaje del commit no puede ser vacío.
```
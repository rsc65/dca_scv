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
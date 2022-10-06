Primero se abre docker Desktop y se verifica que esté conectado, despues se abre la terminal (cmd) y ponemos nuestros primeros comandos.
# Comandos de imagenes.
El primer comando que veremos es ´docker images´, este comando nos devuelve un listado completo de todas las imagenes que hayamos descargado en la pc, si es la primera vez que lo usas la lista estará vacia:

<pre>
C:\Users\ricar>docker images
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
</pre>

Para descargar nuestra primera imagen usaremos el siguiente comando ´docker pull node´, las imagenes las descargaremos de [aqui](https://hub.docker.com/), vamos por ejemplo a node y especificamos la que queramos, por ejemplo ´18-alpine3.15´ o no escribimos nada y descargará la mas reciente.

<pre>
C:\Users\ricar>docker pull node
Using default tag: latest
latest: Pulling from library/node
f606d8928ed3: Pull complete
47db815c6a45: Pull complete
bf4849400000: Pull complete
a572f7a256d3: Pull complete
8f7d05258955: Pull complete
3a459f9ab1c6: Pull complete
c37bcb1df089: Pull complete
bf0ef0f2bfc7: Pull complete
9c17ea02add5: Pull complete
Digest: sha256:9d8a6466c6385e05f62f8ccf173e80209efb0ff4438f321f09ddf552b05af3ba
Status: Downloaded newer image for node:latest
docker.io/library/node:latest
</pre>

Ahora que ya está descargada ponemos nuevamente el comando ´docker images´ y tendremos mas o menos lo siguiente:

<pre>
C:\Users\ricar>docker images
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
node         latest    35ff1df466e8   11 hours ago   991MB
</pre>

Veamos ahora la descarga de otra manera, ponemos el comando ´docker pull node:18´, esto nos descarga node js version 18, lo ejecutamos y veremos que se ejecuta inmediatamente 

<pre>
C:\Users\ricar>docker pull node:18
18: Pulling from library/node
Digest: sha256:9d8a6466c6385e05f62f8ccf173e80209efb0ff4438f321f09ddf552b05af3ba
Status: Downloaded newer image for node:18
docker.io/library/node:18
</pre>

si volvemos a poner el comando de ´docker images´ veremos lo siguiente:

<pre>
C:\Users\ricar>docker images
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
node         18        35ff1df466e8   12 hours ago   991MB
node         latest    35ff1df466e8   12 hours ago   991MB
</pre>

Indicandonos que es la misma descarga, lo unico que cambia es la etiqueta.
Si ahora ponemos el comando ´docker pull node:16´, esto nos descarga node js version 16, esta version tardará en descargarse y al ejecutar el comando ´docker images´ veremos lo siguiente:

<pre>
C:\Users\ricar>docker images
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
node         16        7b887b0a0ccc   12 hours ago   853MB
node         18        35ff1df466e8   12 hours ago   991MB
node         latest    35ff1df466e8   12 hours ago   991MB
</pre>

podemos ir a la [pagina](https://hub.docker.com/_/mysql) y dar clic al comando en negro que dice ´docker pull mysql´, lo pegamos en nuestra terminal y listo

<pre>
C:\Users\ricar>docker pull mysql
Using default tag: latest
latest: Pulling from library/mysql
051f419db9dd: Pull complete
7627573fa82a: Pull complete
a44b358d7796: Pull complete
95753aff4b95: Pull complete
a1fa3bee53f4: Pull complete
f5227e0d612c: Pull complete
b4b4368b1983: Pull complete
f26212810c32: Pull complete
d803d4215f95: Pull complete
d5358a7f7d07: Pull complete
435e8908cd69: Pull complete
Digest: sha256:b9532b1edea72b6cee12d9f5a78547bd3812ea5db842566e17f8b33291ed2921
Status: Downloaded newer image for mysql:latest
docker.io/library/mysql:latest
</pre>

Al ejecutar el comando ´docker images´ veremos lo siguiente:

<pre>
C:\Users\ricar>docker images
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
node         16        7b887b0a0ccc   12 hours ago   853MB
node         18        35ff1df466e8   12 hours ago   991MB
node         latest    35ff1df466e8   12 hours ago   991MB
mysql        latest    43fcfca0776d   3 weeks ago    449MB
</pre>

Si queremos eliminar imagenes pondremos el comando ´docker image rm node:16´, se pone el ´:16´ porque es la version que queremos eliminar dado que tenemos 3

<pre>
C:\Users\ricar>docker image rm node:16
Untagged: node:18
</pre>

Al ejecutar el comando ´docker images´ veremos lo siguiente:

<pre>
C:\Users\ricar>docker images
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
node         18        35ff1df466e8   12 hours ago   991MB
node         latest    35ff1df466e8   12 hours ago   991MB
mysql        latest    43fcfca0776d   3 weeks ago    449MB
</pre>

Eliminamos el comando ´docker image rm node:18´

<pre>
C:\Users\ricar>docker image rm node:16
Untagged: node:18
</pre>

Al ejecutar el comando ´docker images´ veremos lo siguiente:

<pre>
C:\Users\ricar>docker images
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
node         latest    35ff1df466e8   12 hours ago   991MB
mysql        latest    43fcfca0776d   3 weeks ago    449MB
</pre>

Eliminamos finalmente todas las imagenes y nos quedamos con lo siguiente:

<pre>
C:\Users\ricar>docker image rm node
Untagged: node:latest
Untagged: node@sha256:9d8a6466c6385e05f62f8ccf173e80209efb0ff4438f321f09ddf552b05af3ba
Deleted: sha256:35ff1df466e834b2408d56faca095d16dc4002cbd3e4c46c15c72e2aaf18afaf
Deleted: sha256:656856318f3d4e5fd94aee74dd6fa164d0583c13ddda35e5668b87725159b536
Deleted: sha256:40d7670e52b83c4516a70cae3effb62b4f0fd12a1eb36cee88c754f1e7fc8c1b
Deleted: sha256:ad1c4607c48fbdfe026a81696a6fdc9bb38503054eec1a8251a8385cde685245
Deleted: sha256:e3ee7ff5aa8303462d037c922115b4a071aae4e34bb4840b974af5611c91992c
Deleted: sha256:a2765eeb674c78da94152fdd59d691503ed4c4121ab83129a89cf63255b1659d
Deleted: sha256:03821bf9263f670d9a4e2658d201ee5d108759403da38272b28127eea46a2134
Deleted: sha256:db24101d3507d0f5370834318c76e7c62c18fba110a844e1796691488c2067ce
Deleted: sha256:b00657a91aea31613d9a8764759a8784f35a4c7ab55299bc4a9fa88d989d5c15
Deleted: sha256:8e079fee21864e07daa88efcf74f23ad5ade697c06417d0c04a45dfe580ab7f3

C:\Users\ricar>docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
mysql        latest    43fcfca0776d   3 weeks ago   449MB

C:\Users\ricar>docker image rm mysql
Untagged: mysql:latest
Untagged: mysql@sha256:b9532b1edea72b6cee12d9f5a78547bd3812ea5db842566e17f8b33291ed2921
Deleted: sha256:43fcfca0776df8e192d1647da2866237fbd9f8e875fb496e4ca887369b2dd995
Deleted: sha256:45d11760ca3e62bb36a589002b413a42c60c9b917b7a089b116c1ab69155aa4d
Deleted: sha256:af1876abdf5bbbef0ac13e24068669d600bf7de8aa74f31a43ae5f56b83331c2
Deleted: sha256:e1668f1334215580aa7a19beef5d1ee6c6ba121c305154f1ddd7253e21bf65e8
Deleted: sha256:91d92a76bd6a29d88aa511715731ac59d1df33c8e4f5b393dbc16c16b9c08b1c
Deleted: sha256:8608eb76a683654e96af6087a19f416c4498e46f1121e15d63d2ce983750a3a2
Deleted: sha256:fd95c084aad87623a6db2c76480f0765e16ae2ba6de68ce1aefdb7ea4e8fe120
Deleted: sha256:968e68a28e13606ce58651654f554c342f51d5f3ea7e792cdcb21809fefe1a4f
Deleted: sha256:15628dda9c1556632ae3577f5dd8ff16c6456fb95da60284783e8c1f89c588ae
Deleted: sha256:49904d4d7d64ce4a3b64466e4d9bdc624fa8acc760c6a622dcbde03a0ada9fed
Deleted: sha256:df0e3d67e1ecb153c572e3110d36a8bbc46ded2dc376395384c6171732241d90
Deleted: sha256:05dc728e5e49b5db657ec403b875f757afdd8d31f624eea76d706d6eee6395b2

C:\Users\ricar>docker images
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
</pre>

# Comandos de contenedores

Para crear un contenedor lo primero que haremos es una imagen, descargamos la imagen mas reciente de mongo con el comando ´docker pull mongo´, una vez descargado comenzamos con nuestro contenedor, escribimos ´docker create mongo´, mongo es el nombre de la imagen que usaremos como base para crear nuestro contenedor, nos devolvera un ID que es el identificador del contenedor que acabamos de crear, lo necesitaremos para ejecutar nuestro contenedor, lo copiamos ´417fce504889b8282125a1793b2d5ddaf60d536fcdc366f37625ca1629229d65´ 
El comando ´docker create mongo´ es una manera mas facil de escribir el comando ´docker container create mongo´
Para ejecutar nuestro contenedor escribimos el siguiente comando ´docker start 417fce504889b8282125a1793b2d5ddaf60d536fcdc366f37625ca1629229d65´, esto nos devolverá nuestro ID ´417fce504889b8282125a1793b2d5ddaf60d536fcdc366f37625ca1629229d65´, para verificar que nuestro contenedor está corriendo usaremos el siguiente comando ´docker ps´, esto nos devolverá lo siguiente:

|Container ID|Image|Command|Created|Status|Ports|Names|
|:-----------:|:----------:|:--------:|:--------:|:--------:|:--------:|:--------:|
|417fce504889|mongo|"docker-entrypoint.s…"|7 minutes ago|Up 2 minutes|27017/tcp|awesome_montalcini|




















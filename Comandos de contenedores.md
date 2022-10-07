# Comandos de contenedores

En estr apartado veremos los siguientes comandos:
  * `docker create <mongo>`
  * `docker container create <mongo>`
  * `docker start <código>`
  * `docker ps`
  * `docker stop <container ID>`
  * `docker ps -a`
  * `docker create --name <mango> mongo`
  * `docker logs <nombre>`
  * `docker logs --follow <nombre>`
  * `docker run <nombre>`
  * `docker run -d <nombre>`

Para crear un contenedor lo primero que haremos es una imagen, para ello descargamos la imagen mas reciente de mongo (por ejemplo) con el comando `docker pull mongo`

<pre>
C:\Users\ricar>docker pull mongo
Using default tag: latest
latest: Pulling from library/mongo
fb0b3276a519: Pull complete
c81bcd64a2d2: Pull complete
45ed91f63dfa: Pull complete
06d1770a2c11: Pull complete
a03d917eab2f: Pull complete
d0226311fde3: Pull complete
cf22b9bccca1: Pull complete
5a4955b612fd: Pull complete
bc8341d9c8d5: Pull complete
Digest: sha256:2ca8fb22c9522b49fd1f5490dee3e7026a4331b9f904d5acf10a9638c1d1539d
Status: Downloaded newer image for mongo:latest
docker.io/library/mongo:latest
</pre>

Una vez descargada nuestra imagen comenzamos con nuestro contenedor, escribimos `docker create mongo`, siendo mongo el nombre de la imagen que usaremos como base para crear nuestro contenedor

<pre>
C:\Users\ricar>docker create mongo
417fce504889b8282125a1793b2d5ddaf60d536fcdc366f37625ca1629229d65
</pre>

Inmediatamente nos devolvera un ID que es el identificador del contenedor que acabamos de crear, lo copiamos pues lo necesitaremos para ejecutar nuestro contenedor más adelante `417fce504889b8282125a1793b2d5ddaf60d536fcdc366f37625ca1629229d65`

El comando `docker create mongo` es una manera mas facil de escribir el comando `docker container create mongo`

Para ejecutar nuestro contenedor escribimos el siguiente comando `docker start 417fce504889b8282125a1793b2d5ddaf60d536fcdc366f37625ca1629229d65`, esto nos devolverá nuestro ID

<pre>
C:\Users\ricar>docker start 417fce504889b8282125a1793b2d5ddaf60d536fcdc366f37625ca1629229d65
417fce504889b8282125a1793b2d5ddaf60d536fcdc366f37625ca1629229d65
</pre>

Para verificar que nuestro contenedor está corriendo usaremos el siguiente comando `docker ps`, esto nos devolverá lo siguiente:

<pre>
C:\Users\ricar>docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS       NAMES
417fce504889   mongo     "docker-entrypoint.s…"   7 minutes ago   Up 2 minutes   27017/tcp   awesome_montalcini
</pre>

Para detener nuestro contenedor bastará con poner el siguiente comando `docker stop 417fce504889`, nos devolverá el mismo comando que ingresamos

<pre>
C:\Users\ricar>docker stop 417fce504889
417fce504889
</pre>

Si ejecutamos el comando de `docker ps` nos devolverá lo siguiente, indicandonos que nuestro contenedor dejó de correr

<pre>
C:\Users\ricar>docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
</pre>

Cabe mencionar que el contendor sigue existiendo, pero no ejecutandose. Si queremos ver todos los contenedores usaremos el siguiente comando `docker ps -a` (PORTS nos indica si está corriendo)

<pre>
C:\Users\ricar>docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED       STATUS                     PORTS     NAMES
417fce504889   mongo     "docker-entrypoint.s…"   2 hours ago   Exited (0) 5 minutes ago             awesome_montalcini
</pre>

podemos eliminar la imagen usando su nombre y al verificarlo ya no lo encontraremos

<pre>
C:\Users\ricar>docker rm awesome_montalcini
awesome_montalcini

C:\Users\ricar>docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
</pre>

Para asignar un nombre a un contenedor ejecutamos el comando `docker create`, pero agregamos la linea `--name <nombre>` y la imagen en la cual estará basada `mongo` devolviendonos nuevamente un ID. con esto ya no es necesario referenciar con el ID, sino con el nombre que le pusimos

<pre>
C:\Users\ricar>docker create --name mango mongo
ee30607d07ed8612c0d7c7d02925280753b6654a514ddd418b3e3b134a5ad0c5
</pre>

Iniciemos ahora nuestro contenedor con el nombre que le pusimos

<pre>
C:\Users\ricar>docker start mango
mango
</pre>

Veamos ahora como se ve con el comando `docker ps`

<pre>
C:\Users\ricar>docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS          PORTS       NAMES
ee30607d07ed   mongo     "docker-entrypoint.s…"   4 minutes ago   Up 38 seconds   27017/tcp   mango
</pre>

**Sin embargo**, si nosotros intentamos acceder al contenedor para usar mongo y empezar a guardar datos no podremos dado que no hay puertos abiertos para poder usarlo, si queremos hacer uso de un puerto deberemos indicar el puerto de nuestra maquina, mapeando para usarlo (Port mapping). detengamos ahora nuestro contenedor.

<pre>
C:\Users\ricar>docker stop mango
mango
</pre>

## Mapeando puertos

Para mapear puertos usaremos el comando `docker create -p27017:27017` siendo el primero el puerto donde está instalado docker y el segundo el que mapearemos, despues podemos indicarle el nombre que queremos que tenga, nos devolverá un ID, tambien puedes usar el comando `docker create -p27017`

<pre>
C:\Users\ricar>docker create -p27017:27017 --name manguito mongo
f7b00cea5c5dd509f1ed0d6f1dab12b227b80b2975349e06bce280d1c2398790
</pre>

Ingresamos el comando `docker ps` para visualizar el puerto 

<pre>
C:\Users\ricar>docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED              STATUS          PORTS                      NAMES
f7b00cea5c5d   mongo     "docker-entrypoint.s…"   About a minute ago   Up 35 seconds   0.0.0.0:50697->27017/tcp   manguito
</pre>

En algunos casos el puerto no se visualiza, si eso pasa primero debes ejecutar el comando `docker start manguito` antes del comando `docker ps` para que pueda funcionar y logres visualizar el puerto.

Si queremos saber si nuestro contenedor se ejecuto correctaente usaremos el comando `docker logs manguito`

<pre>
C:\Users\ricar>docker logs manguito
{"t":{"$date":"2022-10-07T00:04:17.428Z"},"s":"I",  "c":"NETWORK",  "id":4915701, "ctx":"-","msg":"Initialized wire specification","attr":{"spec":{"incomingExternalClient":{"minWireVersion":0,"maxWireVersion":17},"incomingInternalClient":{"minWireVersion":0,"maxWireVersion":17},"outgoing":{"minWireVersion":6,"maxWireVersion":17},"isInternalClient":true}}}
{"t":{"$date":"2022-10-07T00:04:17.574+00:00"},"s":"I",  "c":"CONTROL",  "id":23285,   "ctx":"main","msg":"Automatically disabling TLS 1.0, to force-enable TLS 1.0 specify --sslDisabledProtocols 'none'"...
</pre>

Sin embargo, si nos manda inmediatamente a la linea de comando, tenemos que usar otro codigo `docker logs --follow manguito`

<pre>
C:\Users\ricar>docker logs --follow manguito
{"t":{"$date":"2022-10-07T00:04:17.428Z"},"s":"I",  "c":"NETWORK",  "id":4915701, "ctx":"-","msg":"Initialized wire specification","attr":{"spec":{"incomingExternalClient":{"minWireVersion":0,"maxWireVersion":17},"incomingInternalClient":{"minWireVersion":0,"maxWireVersion":17},"outgoing":{"minWireVersion":6,"maxWireVersion":17},"isInternalClient":true}}}
{"t":{"$date":"2022-10-07T00:04:17.574+00:00"},"s":"I",  "c":"CONTROL",  "id":23285,   "ctx":"main","msg":"Automatically disabling TLS 1.0,-...
</pre>

Para salir solo presionamos `ctrl + c`, ahora detenemos y eliminamos nuestro contenedor asi como nuestras imagenes 

<pre>
C:\Users\ricar>docker stop manguito
manguito

C:\Users\ricar>docker rm manguito
manguito

C:\Users\ricar>docker image rm mongo
Untagged: mongo:latest
Untagged: mongo@sha256:2ca8fb22c9522b49fd1f5490dee3e7026a4331b9f904d5acf10a9638c1d1539d
Deleted: sha256:1cca5cf682396e2ad3b4af822f1e0f64990a940cf9047c8d93b63af592e054aa
Deleted: sha256:81346ad750a5bb09282a29ae05c55541f9124fc48964edb7889b0d4ea6d68ed0
Deleted: sha256:db6592c1bab79aef8066743c4035e5cb7ff1b0a9143c4bc7a06df018128f3fb9
Deleted: sha256:0469866ca860cc82430f68679b68cd2b0112d3ca0430dced4fc6874e1603628e
Deleted: sha256:84b88272b76ab48f44de70582551f215a132c9cc1555ebcf06cc6bfcbac84253
Deleted: sha256:307ca762a0af14ee827670d10d6e7a3290cc5d34bdbfca3d7dde5b28cd3980ab
Deleted: sha256:fc958d59664e6cd5b50753162597ace373d421c76b8843e2ae4e5a0c71aa9a89
Deleted: sha256:056f42ef32fc14b0488e78642abe96abf6a847a4c0018267634ab0f6252e6c6f
Deleted: sha256:e13a93ec040c0081e6125b52744bfc36e656b97b8f930b65141db771daee7dea
Deleted: sha256:cdca8156a203b9719f985c3114336529115cdc392f89d45cfcd37c968ddd3645
</pre>

Vayamos con el siguiente comando que es la combinaciòn de pull, create y start `docker run <nombre>`, lo primero que hara sera ver si la imagen se encuentra descaergada, sino la descargara, despues creara un contenedor y finalmente lo iniciara

<pre>
C:\Users\ricar>docker run mongo
Unable to find image 'mongo:latest' locally
latest: Pulling from library/mongo
fb0b3276a519: Pull complete
c81bcd64a2d2: Pull complete
45ed91f63dfa: Pull complete
06d1770a2c11: Pull complete
a03d917eab2f: Pull complete
d0226311fde3: Pull complete
cf22b9bccca1: Pull complete
5a4955b612fd: Pull complete
bc8341d9c8d5: Pull complete
Digest: sha256:2ca8fb22c9522b49fd1f5490dee3e7026a4331b9f904d5acf10a9638c1d1539d
Status: Downloaded newer image for mongo:latest
{"t":{"$date":"2022-10-07T00:21:59.637+00:00"},"s":"I",  "c":"CONTROL",  "id":23285,   "ctx":"main","msg":"Automatically disabling TLS 1.0, to force-enable TLS 1.0 specify --sslDisabledProtocols 'none'"}
{"t":{"$date":"2022-10-07T00:21:59.637+00:00"},"s":"I",  "c":"NETWORK",  "id":4915701, "ctx":"main","msg":"Initialized wire specification","attr":{"spec":{"incomingExternalClient":{"minWireVersion":0,"maxWireVersion":17},"incomingInternalClient":{"minWireVersion":0,"maxWireVersion":17},"outgoing":{"minWireVersion":6,"maxWireVersion":17},"isInternalClient":true}}}...
</pre>

Si queremos ejecutarlo de modo "DeHached" (sin mostrar logs) `docker run -d mongo` y nos devolvera el ID del contenedor

<pre>
C:\Users\ricar>docker run -d mongo
1872bd4a91d77570c9181c15145a9644cf02f05b87cfbd753c74bf90822c77f2
</pre>

Si ejecutamos el comando `docker ps` lo encontraremos corriendo con un nombre asignado

<pre>
C:\Users\ricar>docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED              STATUS              PORTS       NAMES
1872bd4a91d7   mongo     "docker-entrypoint.s…"   About a minute ago   Up About a minute   27017/tcp   priceless_sutherland
</pre>

Si queremos asignarle un nombre, un puerto, sin mostrar logs haremos lo siguiente:

<pre>
C:\Users\ricar>docker run --name manguito -p27017:27017 -d mongo
515a1dda650f1cc817e6a1d766a9bf15dd1f106261fbe0d61ff232147013f4e7
</pre>

Nos devolvera el ID y ejecutamos nuevamente `docker ps`

<pre>
C:\Users\ricar>docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                      NAMES
515a1dda650f   mongo     "docker-entrypoint.s…"   53 seconds ago   Up 50 seconds   0.0.0.0:27017->27017/tcp   manguito
</pre>

finalmente eliminamos todo 

<pre>
C:\Users\ricar>docker rm manguito
manguito

C:\Users\ricar>docker image rm mongo
Untagged: mongo:latest
Untagged: mongo@sha256:2ca8fb22c9522b49fd1f5490dee3e7026a4331b9f904d5acf10a9638c1d1539d
Deleted: sha256:1cca5cf682396e2ad3b4af822f1e0f64990a940cf9047c8d93b63af592e054aa
Deleted: sha256:81346ad750a5bb09282a29ae05c55541f9124fc48964edb7889b0d4ea6d68ed0
Deleted: sha256:db6592c1bab79aef8066743c4035e5cb7ff1b0a9143c4bc7a06df018128f3fb9
Deleted: sha256:0469866ca860cc82430f68679b68cd2b0112d3ca0430dced4fc6874e1603628e
Deleted: sha256:84b88272b76ab48f44de70582551f215a132c9cc1555ebcf06cc6bfcbac84253
Deleted: sha256:307ca762a0af14ee827670d10d6e7a3290cc5d34bdbfca3d7dde5b28cd3980ab
Deleted: sha256:fc958d59664e6cd5b50753162597ace373d421c76b8843e2ae4e5a0c71aa9a89
Deleted: sha256:056f42ef32fc14b0488e78642abe96abf6a847a4c0018267634ab0f6252e6c6f
Deleted: sha256:e13a93ec040c0081e6125b52744bfc36e656b97b8f930b65141db771daee7dea
Deleted: sha256:cdca8156a203b9719f985c3114336529115cdc392f89d45cfcd37c968ddd3645
</pre>

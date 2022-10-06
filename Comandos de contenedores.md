# Comandos de contenedores

En estr apartado veremos los siguientes comandos:
  * `docker create <mongo>`
  * `docker container create <mongo>`
  * `docker start <código>`
  * `docker ps`
  * `docker stop <container ID>`
  * `docker ps -a`
  * `docker create --name <mango> mongo`

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

Para mapear puertos usaremos el comando `docker creat -p27017:27017` siendo el primero el puerto donde está instalado docker y el segundo el que mapearemos, despues podemos indicarle el nombre que queremos que tenga, nos devolverá un ID

<pre>

</pre>


<pre>

</pre>

















# Conectandose a los contenedores

En este apartado veremos los siguientes comandos:
  * `-e MONGO_INITDB_ROOT_USERNAME=<nombre>`
  * `-e MONGO_INITDB_ROOT_PASSWORD=<contraseña>`
  * `docker network ls`
  * `docker network create <nombre>`
  * `docker network rm <nombre>`
  * `docker build`

Para conectarnos a un contenedor podemos guiarnos de la pagina de [Docker Hub](https://hub.docker.com/_/mongo), sin embargo seguiremos con el ejemplo, primero descargamos `mongo`, veremos que solo tenemos la imagen de `mongo` sin ningun contenedor

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

C:\Users\ricar>docker images
REPOSITORY   TAG       IMAGE ID       CREATED      SIZE
mongo        latest    1cca5cf68239   2 days ago   695MB

C:\Users\ricar>docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
</pre>

Ahora crearemos nuestro contenedor configurado, le pasaremos las variables de entorno que encontramos en la documentacion de mongo en Docker `-e MONGO_INITDB_ROOT_USERNAME=Rich` y `-e MONGO_INITDB_ROOT_PASSWORD=contraseña`, nos devolvera un ID, escribimos el comando `docker ps -a` y veremos nuestro contenedor y finalmente lo iniciamos para despues verificar que este corriendo

<pre>
C:\Users\ricar>docker create -p27017:27017 --name manguito mongo -e MONGO_INITDB_ROOT_USERNAME=Rich -e MONGO_INITDB_ROOT_PASSWORD=contraseña mongo
8111d90061300e6c8e4c1d98a2e7e26c218060e2d12f0d0c364c302e425e8ec3

C:\Users\ricar>docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED              STATUS    PORTS     NAMES
8111d9006130   mongo     "docker-entrypoint.s…"   About a minute ago   Created             manguito

C:\Users\ricar>docker start manguito
manguito

C:\Users\ricar>docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS                     PORTS     NAMES
8111d9006130   mongo     "docker-entrypoint.s…"   4 minutes ago   Exited (2) 6 seconds ago             manguito
</pre>

A partir de aqui seguiremos una parte de un [Tutorial](https://www.youtube.com/watch?v=4Dko5W96WHg&list=WL&index=15&t=2771s)

Despues de ese pequeño apartado hacemos lo siguiente:
En nuestro editor de texto creamos un archivo llamado `Dockerfile` ese sera su nombre, no puede ser otro, e ingresamos a el, aqui comenzamos con las configuraciones de nuestro contenedor. Primero indicamos la imagen base

<pre>
FROM node:18 #Especificamos la etiqueta de la imagen que queremos usar, en este caso 18
</pre>

Ahora indicamos la carpeta en la que introduciremos el codigo fuente de nuestra aplicacion, pero debemos indicarle de donde sacara el codigo fuente del contenedor

<pre>
RUN mkdir -p /home/app # Nos permite ejecutar instrucciones del sistema operativo Linux

COPY . /home/app # Nos permite acceder a los archivos de nuestro sistema operativo anfitrion (En este caso Windows) para tomarlos dentro del archivo y nuestro contenedor
</pre>

Ahora debemos exponer un puerto para que todos nos podamos conectar al contenedor

<pre>
EXPOSE 3000
</pre>

Indicamos el comando que debemos ejecutar para que nuestra instruccion corra

<pre>
CMD ["node", "/home/app/index.js"] #comando y argumento
</pre>

Ahora podemos guardar, pero no crear la imagen de nuestro contenedor pues necesitamos crear una red en primer instancia para que los contenedores se comuniquen entre si.

`docker network ls` este comando listara todas las redes que tiene configurado docker

<pre>
C:\Users\ricar>docker network ls
NETWORK ID     NAME      DRIVER    SCOPE
0ffddfecca4e   bridge    bridge    local
58251f05f61f   host      host      local
3a2dc677336c   none      null      local
</pre>

Para crear nuestr propia red usamos el siguiente comando `docker network create MiRed`, nos devolvera el ID de la red y al inspeccionar con el comando `docker network ls` veremos nuestra red

<pre>
C:\Users\ricar>docker network create MiRed
b7b568db849965bfc151181a7b1020869c64b2d34212547b6f2294e20a8ff816

C:\Users\ricar>docker network ls
NETWORK ID     NAME      DRIVER    SCOPE
b7b568db8499   MiRed     bridge    local
0ffddfecca4e   bridge    bridge    local
58251f05f61f   host      host      local
3a2dc677336c   none      null      local
</pre>

Si la queremos eliminar usamos el comando `docker network rm MiRed` y veremos que ha desaparecido

<pre>
C:\Users\ricar>docker network rm MiRed
MiRed

C:\Users\ricar>docker network ls
NETWORK ID     NAME      DRIVER    SCOPE
0ffddfecca4e   bridge    bridge    local
58251f05f61f   host      host      local
3a2dc677336c   none      null      local
</pre>

Ahora regresamos a nuestro editor de texto en `index.js` cambiamos la ruta de conexion por el nombre de nuestro contenedor (manguito)
`docker build` con este comando creamos imagenes en base a un archivo dockerfile, en este caso no se mostrara nada porque no tenemos una aplicacion, este comando recibe dos argumentos, el nombre de la imagen y el segundo la ruta de nuestro proyecto 

<pre>
C:\Users\ricar>docker build
"docker build" requires exactly 1 argument.
See 'docker build --help'.

Usage:  docker build [OPTIONS] PATH | URL | -

Build an image from a Dockerfile

C:\Users\ricar>docker build -t miapp:loquequieras . # el punto es la ruta que es donde estamos actualmente
[+] Building 2.5s (2/2) FINISHED
 => [internal] load build definition from Dockerfile                                                               2.5s
 => => transferring dockerfile: 2B                                                                                 0.4s
 => [internal] load .dockerignore                                                                                  2.1s
 => => transferring context: 2B                                                                                    0.3s
failed to solve with frontend dockerfile.v0: failed to read dockerfile: open /var/lib/docker/tmp/buildkit-mount791092371/Dockerfile: no such file or directory
</pre>

Volvemos con el comando de `docker images` y veremos que se ha creado nuestra imagen 

<pre>
C:\Users\ricar>docker images
REPOSITORY   TAG          IMAGE ID       CREATED        SIZE
manguito     loquequieras 8o7q28fne4vh   5 seconds ago  961MB
mongo        latest       1cca5cf68239   2 days ago     695MB
</pre>

Ahora crearemos nuestro contenedor de mongo asignandole nuestra red con el siguiente codigo `docker create -p27017:27017 --name manguito --network mired -e MONGO_INITDB_ROOT_USERNAME=Rich -e MONGO_INITDB_ROOT_PASSWORD=contraseña mongo`

<pre>
C:\Users\ricar>docker create -p27017:27017 --name manguito --network mired -e MONGO_INITDB_ROOT_USERNAME=Rich -e MONGO_INITDB_ROOT_PASSWORD=contraseña mongo
415877b5aa0502a880a6a88925270408593d7f5e03d7beecb94e31afa4ebbfa2
</pre>

Ahora creamos el contenedor de la aplicacion que colocamos dentro de una imagen con el comando `docker create -p3000:3000 --name chanchito --network mired miapp:loquequieras`, en nuestro caso no funciona porque no tenemos la app jeje y vemos que nuestra app ya tiene asignada nuestra red

<pre>
C:\Users\ricar>docker create -p3000:3000 --name chanchito --network mired miapp:loquequieras
Unable to find image 'miapp:loquequieras' locally

C:\Users\ricar>docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS    PORTS     NAMES
415877b5aa05   mongo     "docker-entrypoint.s…"   4 minutes ago   Created             manguito
#Aqui estaria si tuviera la app...#
</pre>

Ahora iniciamos nuestros contenedores

<pre>
C:\Users\ricar>docker start manguito
manguito

C:\Users\ricar>docker start chanchito
chanchito
</pre>

Y finalmente corroboramos que nuestro contenedor està corriendo

<pre>
C:\Users\ricar>docker logs chanchito
</pre>

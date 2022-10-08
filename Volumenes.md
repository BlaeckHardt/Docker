# Volumenes

Con los voluenes, un parte de nuestros archivos dentro de nuestro contenedor los podemos tener en una carpeta de nuestro sistema operativo anffitrion, no en el contenedor, a manera que si eliminamos nuestro contenedor los datos persistiran. Esto es util para bases de datos y para cuando estas desarrollando. Asi mismo tenemos tres tipos de volumenes:

* Anonimo: solo indicas la ruta: no se pueden referenciar para ser usados por otro contenedor
* De anfitrion o host: decides que carpeta y donde montarla
* Nombrado: Es como el anonimo, pero se puede referenciar 

En este apartado veremos los siguientes comandos:
  * `docker create <mongo>`

Regresamos a nuestra carpeta de `docker-compose` a definir nuestros volumenes

<pre>
version: "3.9"
services:
  chanchito:
    build: .
    ports: 
      - "3000:3000"
    links:
      - manguito
  manguito:
    image: mongo
    ports: 
      - "27017:27017"
    environment:
      - MONGO_INITDB_ROOT_USERNAME=Rich
      - MONGO_INITDB_ROOT_PASSWORD=contraseña
</pre>

Agregaremos las siguientes lineas

<pre>
version: "3.9"
services:
  chanchito:
    build: .
    ports: 
      - "3000:3000"
    links:
      - manguito
  manguito:
    image: mongo
    ports: 
      - "27017:27017"
    environment:
      - MONGO_INITDB_ROOT_USERNAME=Rich
      - MONGO_INITDB_ROOT_PASSWORD=contraseña
    volmes: 
      - mongo-data: /data/db #este es para mongo db
      # para mysql: /var/lib/mysql
      # para postgres: /var/lib/postgresql/data
      - otro-volumen: /data/db #imaginemos que este tambien es para mongo db
      
volumes: 
  mongo-data:
  otro-volumen:
</pre>

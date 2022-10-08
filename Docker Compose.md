# Introduccion

El proceso al trabajar con contenedores es el siguiente: (por cada contenedor)
  * Descargar una imagen basada en Linux
  * Crear una red
  * Crear el contenedor
    * Asignar puertos
    * Asignar nombres 
    * Asignar varianles de entorno
    * Especificar la red
    * Indicar la imagen: con su etiqueta
Afortunadamenter tenemos una herramienta que nos ahorra todo eso.

Los comandos en este apartado son:
 * `docker compose up`
 * `docker compose down`

# Docker compose

Empezaremos desde nuestro editor de texto, crearemos una carpeta de nombre `docker-compose.yml`, a partir de aqui en nuestro editor de texto agregaremos las siguientes lineas

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

Guardamos y regresamos a CMD

`docker compose up` este comando hace lo mismo que lo que acabamos de hacer, pero el CMD, una vez ejecutado veremos los logs. Detenemos con `ctrl+c` y al verificar con `docker images` veremos una nueva imagen de nombre (en este caso) de `mongoapp_chanchito`. Si queremos eliminar los contenedores que hemos creado y su imagen, usaremos el comando `docker compose down`

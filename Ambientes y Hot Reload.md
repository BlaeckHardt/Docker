# Ambientes y Hot Reload

Si queremos agilizar el desarrollo haremos lo siguiente:

Regresamos a nuestro editor de texto y crearemos un nuevo archivo `Dockerfile.dev` copiamos lo que teniamos en el archivo `Dockerfile.dev` y guardamos

<pre>
FROM node:18

RUN npm i -g nodemon
RUN mkdir -p /home/app

WORKDIR /home/app

EXPOSE 3000

CMD ["nodemon", "index.js"]
</pre>

Ahora agregamos otro archivo nuevo de nombre `docker-compose-dev.yml` y copiamos todo lo que teniamos en `docker-compose.yml` y guardamos

<pre>
version: "3.9"
services:
  chanchito:
    build:
      context: .
      dockerfile: Dockerfile.dev
    ports: 
      - "3000:3000"
    links:
      - manguito
    volumes: #volumen anonimo
      - .:/home/app
  manguito:
    image: mongo
    ports: 
      - "27017:27017"
    environment:
      - MONGO_INITDB_ROOT_USERNAME=Rich
      - MONGO_INITDB_ROOT_PASSWORD=contraseña
</pre>

Regresamos a CMD y escribimos el comando `docker compose -f docker-compose-dev.yml up`

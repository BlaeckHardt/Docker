# Comandos de contenedores

Para crear un contenedor lo primero que haremos es una imagen, descargamos la imagen mas reciente de mongo con el comando ´docker pull mongo´, una vez descargado comenzamos con nuestro contenedor, escribimos ´docker create mongo´, mongo es el nombre de la imagen que usaremos como base para crear nuestro contenedor, nos devolvera un ID que es el identificador del contenedor que acabamos de crear, lo necesitaremos para ejecutar nuestro contenedor, lo copiamos ´417fce504889b8282125a1793b2d5ddaf60d536fcdc366f37625ca1629229d65´ 
El comando ´docker create mongo´ es una manera mas facil de escribir el comando ´docker container create mongo´
Para ejecutar nuestro contenedor escribimos el siguiente comando ´docker start 417fce504889b8282125a1793b2d5ddaf60d536fcdc366f37625ca1629229d65´, esto nos devolverá nuestro ID ´417fce504889b8282125a1793b2d5ddaf60d536fcdc366f37625ca1629229d65´, para verificar que nuestro contenedor está corriendo usaremos el siguiente comando ´docker ps´, esto nos devolverá lo siguiente:

|Container ID|Image|Command|Created|Status|Ports|Names|
|:-----------:|:----------:|:--------:|:--------:|:--------:|:--------:|:--------:|
|417fce504889|mongo|"docker-entrypoint.s…"|7 minutes ago|Up 2 minutes|27017/tcp|awesome_montalcini|





















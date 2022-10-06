# Docker

## Contenedores

Son una forma de empaquetar aplicaciones con todas las dependencias que este tenga incluyendo sus archivos de configuración, es como tener una caja en la que tendremos código en cualquier lenguaje que usemos, etc. Los contenedores son portables, es decir, faciles de compartir con otros desarrolladores y entre el equipo de operaciones volviendo el desarrolllo y despliegue de nuestras aplicaciones sea más fácil.

## ¿Dónde se almacenan?

Se almacenan en un repositorio de contenedores (como un github), estos pueden ser tanto públicos como privados, el repositorio público más conocido es [Docher Hub](https://hub.docker.com/) en donde encontraremos aplicaciones como:
  * `Node JS`
  * `Python`
  * `MySQL`
  * `Postgres`
  * `Golang`
  * Y distintas distribuciones de Linux

## Trabajando con Contenedores

El proceso al trabajar con contenedores es el siguiente:
  * Descargar una imagen basada en Linux

## Ventajas de usar contenedores

Entre las principales ventajas de trabajar con contenedores está el permitir que desarrolladores y operadores trabajen en conjunto de construir una imagen.
Pesan poco comparado con las máquinas virtuales (que pueden pesar GB en lugar de MB).

## Imagen

Es el empaquetado que contiene las dependencias y el código, siendo la imagen lo que se comparte y con la cual ejecutamos un comando que mantiene las dependencias corriendo en conjunto con su entorno, variables de entorno, entre otros. 

## Container

Un container son capas de imagenes, donde la capa más baja será por lo general una distribución de Linux siendo `Alpine Linux` la más utilizada (esto debido a que es considerablemente liviana). 

## Virtualización

Existen 3 tipos de virtualización:

  * Paravistualización: trata de entregar la mayor cantidad de acceso por parte del sistema operativo anfitrion [por ejemplo Ubuntu] a los clientes [por ejemplo Ubuntu, Debian, Suse]
  * Vitualización parcial: Donde algunos componentes del Hardware se  virtualizan para el sistema operativo cliente.
  * Virtualización completa: Donde absolutamente todos los componentes o Hardware usado por el sistema operativo cliente son virtualizados de manera que los sistemas operativos cliente no acceden al Hardware.
Docker es una forma de virtualización, usa el kernel del sistema operativo anfitrión traduciendose en que la imagen usa menos espacio, así como rendimiento muy superior a todas las alternativas de virtualización. Veamos la comparación entre una VM (Virtual Machine) contra Docker.

Virtual Machine:

  * Se compone de 3 capas:
    * Su primera capa es al Hardware de donde se va a ejecutar
    * Su segunda capa es el Kernel, el encargado de comunicarse con el Hardware
    * Su tercera capa son las aplicaciones que estamos utilizando 
  * Generalmente lo que tenemos visualizado son las aplicaciones y el kernel haciendo que nuestras imagenes pesen GB

Docker

  * Solo se visualiza la capa de aplicaciones
  * Usa el kernel del sistema operativo en que se está ejecutando 

## Para empezar a trabajar

Descargamos e instalamos [Docker Desktop](https://www.docker.com/products/docker-desktop/) siguiendo todas las instrucciones, una vez instalado abrimos la aplicación y nos fijamos que esté conectado para poder empezar y una vez hecho esto procedemos a abrir la terminal `cmd` para ejecutar nuestros comandos.

## Comandos de Docker y más

<pre>
Management Commands:
  builder     Manage builds
  buildx*     Docker Buildx (Docker Inc., v0.9.1)
  compose*    Docker Compose (Docker Inc., v2.10.2)
  config      Manage Docker configs
  container   Manage containers
  context     Manage contexts
  extension*  Manages Docker extensions (Docker Inc., v0.2.9)
  image       Manage images
  manifest    Manage Docker image manifests and manifest lists
  network     Manage networks
  node        Manage Swarm nodes
  plugin      Manage plugins
  sbom*       View the packaged-based Software Bill Of Materials (SBOM) for an image (Anchore Inc., 0.6.0)
  scan*       Docker Scan (Docker Inc., v0.19.0)
  secret      Manage Docker secrets
  service     Manage services
  stack       Manage Docker stacks
  swarm       Manage Swarm
  system      Manage Docker
  trust       Manage trust on Docker images
  volume      Manage volumes

Commands:
  attach      Attach local standard input, output, and error streams to a running container
  build       Build an image from a Dockerfile
  commit      Create a new image from a container's changes
  cp          Copy files/folders between a container and the local filesystem
  create      Create a new container
  diff        Inspect changes to files or directories on a container's filesystem
  events      Get real time events from the server
  exec        Run a command in a running container
  export      Export a container's filesystem as a tar archive
  history     Show the history of an image
  images      List images
  import      Import the contents from a tarball to create a filesystem image
  info        Display system-wide information
  inspect     Return low-level information on Docker objects
  kill        Kill one or more running containers
  load        Load an image from a tar archive or STDIN
  login       Log in to a Docker registry
  logout      Log out from a Docker registry
  logs        Fetch the logs of a container
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  ps          List containers
  pull        Pull an image or a repository from a registry
  push        Push an image or a repository to a registry
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  rmi         Remove one or more images
  run         Run a command in a new container
  save        Save one or more images to a tar archive (streamed to STDOUT by default)
  search      Search the Docker Hub for images
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  version     Show the Docker version information
  wait        Block until one or more containers stop, then print their exit codes
</pre>

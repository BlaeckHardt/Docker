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

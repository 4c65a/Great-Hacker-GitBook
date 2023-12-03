# Docker

## CheatSheetDocker

## Comandos básicos

**docker run**: Ejecuta un contenedor. Ejemplo: docker run nginx

**docker start**: Inicia un contenedor previamente creado. Ejemplo: docker start my\_container

**docker stop**: Detiene un contenedor en ejecución. Ejemplo: docker stop my\_container

**docker rm**: Elimina un contenedor. Ejemplo: docker rm my\_container

**docker ps**: Muestra los contenedores en ejecución. Ejemplo: docker ps

**docker images**: Muestra las imágenes disponibles en el host. Ejemplo: docker images

**docker pull**: Descarga una imagen de un repositorio. Ejemplo: docker pull ubuntu

## Trabajo con imágenes

**docker build**: Crea una imagen a partir de un archivo Dockerfile. Ejemplo: docker build -t my\_image

**docker tag**: Etiqueta una imagen con un nombre personalizado. Ejemplo: docker tag my\_image my\_registry/my\_image:1.0

**docker push**: Envía una imagen a un repositorio. Ejemplo: docker push my\_registry/my\_image:1.0

**docker rmi**: Elimina una imagen. Ejemplo: docker rmi my\_image

## Redes y volúmenes

**docker network create**: Crea una red personalizada. Ejemplo: docker network create my\_network

**docker network connect**: Conecta un contenedor a una red existente. Ejemplo: docker network connect my\_network my\_container

**docker volume create**: Crea un volumen personalizado. Ejemplo: docker volume create my\_volume

**docker volume ls**: Muestra los volúmenes disponibles. Ejemplo: docker volume ls

**docker volume rm**: Elimina un volumen. Ejemplo: docker volume rm my\_volume

## Comandos avanzados

**docker exec**: Ejecuta un comando en un contenedor en ejecución. Ejemplo: docker exec my\_container ls /

**docker logs**: Muestra los registros de un contenedor en ejecución. Ejemplo: docker logs my\_container

**docker inspect**: Muestra información detallada sobre un contenedor o imagen. Ejemplo: docker inspect my\_container

**docker commit**: Crea una nueva imagen a partir de los cambios en un contenedor en ejecución. Ejemplo: docker commit my\_container my\_image

**docker-compose**: Herramienta para definir y ejecutar aplicaciones Docker multi-contenedor. Ejemplo: docker-compose up -d

####


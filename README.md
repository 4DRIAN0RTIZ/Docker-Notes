# Docker

## Glosario de términos

- Docker: Herramienta diseñada para facilitar la creación, implementación, y ejecución de aplicaciones mediante el uso de contenedores.
- Container: Es una instancia de una imagen, es decir, es la ejecución de una imagen. Se ejecuta en un ambiente aislado.
- Image: Es un paquete de software que contiene todo lo necesario para ejecutar una aplicación, incluyendo código, librerías, variables de entorno, y archivos de configuración. Una fotografía de la versión de las tecnologías completamente funcional.
- Dockerizar: Es el proceso de convertir una aplicación en una imagen de Docker. Se toma un código fuente y genera una imagen lista para montar y correrla en un contenedor.
- Dockerfile: Es un archivo de texto con instrucciones necesarias para crear una imagen. Se puede ver como un script que contiene los pasos necesarios para crear una imagen.
- .dockerignore: Es un archivo que contiene patrones de archivos y directorios que se ignoran al momento del build de la imagen.
- docker-compose.yml: Es un archivo de texto que contiene la configuración necesaria para ejecutar múltiples contenedores como un servicio. Es decir, se puede definir un servicio que contenga múltiples contenedores.
- volume: Es un directorio que se monta en un contenedor. Se utiliza para persistir datos y compartirlos entre contenedores.
- Docker Deamon: Es el servicio en segundo plano que se ejecuta en el host que administra la creación, ejecución y distribución de contenedores Docker.
- Registry: Es una aplicación del lado del servidor altamente escalable y sin estado que almacena y le permite distribuir imágenes de Docker.
- Snyk: Es una plataforma de seguridad para desarrolladores para proteger el código, las dependencias, los contenedores y la infraestructura como código.
- Docker Layers: Las capas son el resultado de la forma en que se construyen las imágenes de Docker. Cada paso es un Dockerfile crea una nueva "capa" que es esencialmente una diferencia de los cambios en el sistema de archivos desde el último paso.


## ¿Qué es Docker y para qué sirve?

Supongamos que un nuevo desarrollador ingresa al proyecto. Será necesario que le indiquemos que dependencias y que tecnologías estamos usando para que pueda ejecutar el proyecto en su máquina. Esto puede ser un proceso largo y tedioso. Además, si el desarrollador trabaja en múltiples proyectos, es posible que se encuentre con problemas de compatibilidad entre versiones de dependencias. O incluso que el desarrollador tenga un sistema operativo diferente al nuestro, lo cual puede generar problemas de compatibilidad.

Docker llega a solucionar este problema. Docker es una herramienta que permite crear, implementar y ejecutar aplicaciones mediante el uso de contenedores. Los contenedores son ambientes aislados que contienen todo lo necesario para ejecutar una aplicación, incluyendo código, librerías, variables de entorno, y archivos de configuración.

No es una máquina virtual, ya que no necesita un sistema operativo completo para funcionar. En cambio, utiliza el sistema operativo del host, lo cual lo hace mucho más ligero y eficiente. Además, los contenedores son portables, es decir, se pueden ejecutar en cualquier máquina que tenga instalado Docker. Sin mencionar que las máquina virtuales son mucho más pesadas y lentas que los contenedores.

### Beneficios de usar Docker

- Cada contenedor está aislado de los demás.
- Es posible ejecutar varias instancias de la misma versión o diferentes versiones sin configuraciones adicionales.
- Con un comando, puedes descargar, levantar y corre todo lo que necesitas.
- Cada contenedor contiene todo lo que necesita para ejecutarse.
- Indiferente el sistema operativo host
- A diferencia de las máquinas virtuales, los contenedores se levantan en milésimas de segundo a unos cuantos segundos.


## Comandos básicos

Ayuda de docker

```bash
docker container --help
```

Iniciar un comando shell dentro del contenedor. `-it` es para una terminal interactiva
```bash
docker exec -it CONTAINER_ID EXECUTABLE 
docker exec -it web bash
docker exec -it web /bin/bash
```

### docker container --help
Comandos:
- attach: Conecta la entrada, salida y error estándar de un contenedor a la terminal actual.
- commit: Crea una nueva imagen a partir de los cambios realizados en un contenedor.
- cp: Copia archivos o carpetas entre el host y el contenedor.
- create: Crea un nuevo contenedor.
- diff: Inspecciona los cambios realizados en el sistema de archivos de un contenedor.
- exec: Ejecuta un comando en un contenedor en ejecución.
- export: Exporta el sistema de archivos de un contenedor como un archivo tar.
- inspect: Muestra información detallada de uno o más contenedores.
- kill: Detiene un contenedor en ejecución enviando una señal SIGKILL.
- logs: Muestra los logs de un contenedor.
- ls: Lista los contenedores.
- pause: Pausa todos los procesos dentro de un contenedor.
- port: Lista los puertos mapeados de un contenedor.
- prune: Elimina los contenedores detenidos.
- rename: Renombra un contenedor.
- restart: Reinicia un contenedor.
- rm: Elimina uno o más contenedores.
- run: Crea un nuevo contenedor y lo ejecuta.
- start: Inicia uno o más contenedores detenidos.
- stats: Muestra las estadísticas de uso de recursos de los contenedores en ejecución.
- stop: Detiene uno o más contenedores en ejecución.
- top: Muestra los procesos en ejecución de un contenedor.
- unpause: Reanuda todos los procesos dentro de un contenedor pausado.
- update: Actualiza la configuración de uno o más contenedores.
- wait: Bloquea hasta que un contenedor se detenga y luego imprime su código de salida.

1. Descargar una imagen
```bash

docker pull IMAGE_NAME // Traer una imagen
docker pull IMAGE_NAME:TAG
docker pull hello-world
docker pull hello-world:15.1
```

2. Ejecutar

```bash
docker run hello-world
```

3. Listar contenedores
```bash
docker ls // Lista los contenedores que se están ejecutando
docker container ls -a // Lista todos los contenedores
```

3. Eliminar
docker container rm CONTAINER_ID // Elimina un contenedor. Se pueden eliminar varios contenedores a la vez. Puedes colocar uniq o los primeros 3 caracteres del id.
```bash
docker container rm c54 e4t
```

Y te devuelve el id del contenedor eliminado.

En caso de querer eliminar una imagen, se debe eliminar primero los contenedores que la usan. Posteriormente se puede eliminar la imagen.
```bash
docker rmi IMAGE_ID // Elimina una imagen. Puenden ser varios ids. Se puede colocar los primeros 3 caracteres del id.
docker image rm IMAGE_ID // Otra forma de eliminar una imagen
```

### Material extra

Existe un contenedor docker/getting-started que contiene una aplicación de ejemplo. Se puede ejecutar con el siguiente comando:
```bash
docker contaier run -dp 80:80 docker/getting-started
```

```bash
docker container run -d docker/getting-started // Ejecuta el contenedor en segundo plano. -d es de detach.
```

```bash
docker container stop CONTAINER_ID // Detiene un contenedor
// Se detiene el contenedor pero no se elimina. Se puede volver a ejecutar con el mismo id.
```

Para levantar y ejecutar el contenedor en segundo plano y mappear el puerto 80 del contenedor al puerto 80 del host:
```bash
docker container run -dp 80:80 docker/getting-started
```

Por mappear se refiere a que el puerto 80 del contenedor se mapea al puerto 80 del host. Es decir, si se accede al localhost:80 se accede al contenedor. Es como unificar los puertos.

Vamos a detener el contenedor:

```bash
docker container stop CONTAINER_ID // Detiene un contenedor
```

Y lo ejecutamos de nuevo:
```bash
docker container start CONTAINER_ID // Inicia un contenedor
```

En dado caso de que se quiera eliminar un contenedor que este en ejecución se debe agregar el flag -f:
```bash
docker container rm -f CONTAINER_ID // Elimina un contenedor
```

## Variables de entorno

Entiéndase las variables de entorno como variables globales que se pueden usar en cualquier lugar del sistema operativo. Éstas variables pueden ser accedidas por cualquier proceso que se ejecute en el sistema operativo. En el siguiente ejemplo se muestra como agregar una variable de entorno al contenedor:
```bash
docker run -d --network app --network-alias mysql -v app-mysql-data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=secret -e MYSQL_DATABASE=todo
```

Vamos a realizar un ejemplo, ingresamos a [dockerhub](https://hub.docker.com/) y buscamos la imagen de postgres. En la sección de tags podemos ver las versiones disponibles. Vamos a usar la versión 5.7.34.

<kbd style="background-color: #CCFFCC;margin-bottom: 10px; padding: 10px; line-height: 1.5;">
<strong>Nota:</strong> Las imágenes oficiales de docker se distinguen por tener una insignia verde al lado del nombre.
</kbd>

Para descargar la imagen usamos el comando:
```bash
docker pull postgres
```

Dependiendo la imagen que se descargue será distinta la manera de proporcionar las variables de entorno, por lo que se recomienda leer la documentación de la imagen que se descargue para conocer la sintaxis correcta.

Siguiendo el ejemplo de postgres, nos conectaríamos al contenedor con el siguiente comando:
```bash
docker container run -d --name postgres -e POSTGRES_PASSWORD=secret postgres
```

Esto nos va a ejecutar el contenedor en segundo plano y nos va a crear una variable de entorno llamada POSTGRES_PASSWORD con el valor secret.

## Usar Imagen

Al aplicar un `docker container ls -a` podemos ver que la instancia de postgres está siendo ejecutada en el puerto 5423. De esta manera no es posible acceder a la base de datos. Para poder acceder a la base de datos se debe mapear el puerto 5423 del contenedor al puerto 5432 del host.

El usuario por defecto por defecto es postgres y la contraseña es la que se le asignó a la variable de entorno POSTGRES_PASSWORD.

Para poder hacer esto es necesario eliminar el contenedor y volverlo a ejecutar con el puerto mapeado. Es necesario primero detener el contenedor y posteriormente eliminarlo. Para detenerlo se usa el comando:
```bash
docker container stop CONTAINER_ID
```

Y para eliminarlo:
```bash
docker container rm CONTAINER_ID
```

<kbd style="background-color: #CCFFCC;margin-bottom: 10px; padding: 10px; line-height: 1.5;">
<strong>Nota:</strong> Si la terminal devuelve el id del contenedor es porque se eliminó correctamente.
</kbd>

Una vez eliminado lo volvemos a ejecutar pero esta vez con los siguientes cambios:

- El puerto 5423 del contenedor se mapea al puerto 5432 del host.

```bash
docker run --name some-postgres -e POSTGRES_PASSWORD=mysecretpassword -dp 5432:5432 postgres
```

Se agrega el parámetro `p 5432:5432` para mapear el puerto 5432 del host al puerto 5432 del contenedor. En ese orden. Es decir, antes de los dos puntos se coloca el puerto del host y después el puerto del contenedor.

Para poder visualizar mejor y de paso aprender un poco más, vamos a instalar postgres en nuestro sistema operativo. Para esto vamos a usar el siguiente comando:
```bash
sudo apt install postgresql-client
```

Una vez instalado con conectamos a la base de datos con el siguiente comando:
```bash
psql -h localhost -p 5432 -U postgres
# postgres es el usuario por defecto
```

Cuando solicite la contraseña, se debe ingresar la contraseña que se le asignó a la variable de entorno POSTGRES_PASSWORD. En este caso es mysecretpassword.

Y vualá, ya estamos conectados a PostgreSQL desde la terminal.

<details>
<summary>Comandos básicos de PostgreSQL</summary>
<ul>
  <li>Crear una base de datos: `CREATE DATABASE nombre_base_datos;`.</li>
  <li>Conecatar a una base de datos: `\c nombre_base_datos`.</li>
  <li> Listar las bases de datos: `\l`.</li>
  <li> Listar las tablas: `\dt`.</li>
  <li> Listar las funciones: `\df`.</li>
  <li> Listar los roles: `\du`.</li>
  <li> Listar las vistas: `\dv`.</li>
  <li> Listar los índices: `\di`.</li>
</details>

---

Creamos una base de datos con el siguiente comando:
```mysql
CREATE DATABASE pruebas;
```

### Múltiples instancias.

En algunas ocasiones será necesario contar con distintas instancias de un mismo servicio, ya sea por que quieres hacer alguna migración o por que estás con otro proyecto y necesitas otra instancia del servicio. 

Vamos a hacer el ejemplo con postgres. Para esto vamos a ejecutar el siguiente comando para crear la primera instancia:

```bash
docker container run \
--name postgres-alpha \
-e POSTGRES_PASSWORD=mypass1 \
-dp 5432:5432 \
postgres
```

<kbd style="background-color: #CCFFCC;margin-bottom: 10px; padding: 10px; line-height: 1.5;">
<strong>Nota:</strong> Se considera buena práctica poner el nombre del contenedor con el nombre del servicio y el sufijo -alpha para indicar que es la primera instancia. Siempre se recomienda poner el tag de la imagen para evitar que se descargue la última versión de la imagen y se pueda generar algún error.
</kbd>

A continuación vamos a crear la segunda instancia, se utilizará la versión 14-alpine3.17 de postgres. Para esto ejecutamos el siguiente comando:
```bash
docker container run \
--name postgres-beta \
-e POSTGRES_PASSWORD=mypass2 \
-dp 5433:5432 \ # Se mapea en un puerto distinto del host
postgres:14-alpine3.17
```

### Logs

Para poder ver lo que está ocurriendo en nuestros contenedores podemos hacer uso de los logs. Para esto usamos el comando:
```bash
docker container logs CONTAINER_ID
docker container logs --follow CONTAINER_ID # Para ver los logs en tiempo real
docker stats # Para ver el uso de recursos de los contenedores
```

Para poder borrar todas las imágenes que no se están usando se usa el siguiente comando:
```bash
docker image prune
```

### Prueba Mysql

Para continuar con las pruebas vamos a descargar la versión jammy de [MariaDB](https://hub.docker.com/_/mariadb).

Esta vez le vamos a pasar unas variables de entorno. Usando `--env`. 

```bash
docker container run -dp 3307:3306 \
--name world-db \
--env MYSQL_USER=admin \
--env MYSQL_PASSWORD=admin123 \
--env MYSQL_ROOT_PASSWORD=root123 \
--env MYSQL_DATABASE=world-db \
mariadb:jammy
```

<kbd style="background-color: #CCFFCC;margin-bottom: 10px; padding: 10px; line-height: 1.5;">
<strong>Nota:</strong> En la documentación oficial hay dos formas de declarar las variables de entorno dependiendo de las instancias que estés usando. Si localmente ya tienes SQL instalado tienes que hacerlo así, en caos contrario únicamente cambia `MYSQL` por `MARIADB` en las variables de entorno.
</kbd>

Para conectarte a mysql se usa la siguiente sintaxis:
```bash
mysql -u admin -p -h 127.0.0.1 -P 3307
```

Vamos a descargar un script de sql para insertar datos genéricos en la base de datos. Descargamos el [world.sql.gz](https://github.com/kakakakakku/mysql-world-database-dockerfiles/blob/master/5.5/world.sql.gz) Y se descomprime con 7z para continuar.

```bash
7z x world.sql.gz
```

Una vez descomprimido lo ejecutamos en nuestra base de datos de la siguiente manera:

```bash
mysql -uroot -h 127.0.0.1 -p world-db < ABSOLUTE_PATH/world.sql
```

## Volúmenes

En docker existen 3 tipos de volúmenes, son usados para hacer persistente de la data entre reinicios y levantamientos de imágenes.

### Named volumes

Este es el volumen más usado. Se crea con el siguiente comando:

- Crear un nuevo volumen: `docker volume create NOMBRE_VOLUMEN`
- Listar los volúmenes: `docker volume ls`
- Inspeccionar el volumen específico: `docker volume inspect NOMBRE_VOLUMEN`
- Remover los volúmenes no usados: `docker volume prune`
- Remueve uno o más volúmenes: `docker volume rm NOMBRE_VOLUMEN`
- Usar un volumen al corre un contenedor: `docker container run -v NOMBRE_VOLUMEN:/ruta/destino CONTAINER_ID`

**Ejemplo:** Vamos a crear un volumen para guardar la data de MariaDB. Para esto vamos a ejecutar el siguiente comando:
```bash
docker container run -dp 3306:3306 \
--name world-db \
--env MYSQL_USER=admin \
--env MYSQL_PASSWORD=admin123 \
--env MYSQL_ROOT_PASSWORD=root123 \
--env MYSQL_DATABASE=world-db \
--volume world-db:/var/lib/mysql \
mariadb:jammy
```

### Bind volumes -- Vincular volúmenes.

Bind volumes trabaja con paths absolutos, es decir, se debe especificar la ruta completa del volumen. Se usa de la siguiente manera:

```bash
docker container run \
--name nest-app \
-w /app \ # Working directory
-p 3000:3000 \
-v "$(pwd)":/app \ # Vincula el directorio actual con el directorio /app del contenedor. Se recomienda usar este comando dentro de la carpeta del proyecto.
node:16-alpine3.16 \
sh -c "yarn install && yarn run dev" # Comando para ejecutar el contenedor.
```

### Anonymous volumes

Volúmenes donde sólo se especifica el path del contenedor y Docker lo asigna automáticamente en el host. Se usa de la siguiente manera:
```bash
docker run -v /var/lib/mysql mysql
```

## PhpMyAdmin

En lo personal siempre he preferido manejar las bases de datos desde la terminal, pero en algunas ocasiones es necesario usar un gestor de bases de datos. Para esto vamos a usar PhpMyAdmin. Posiblemente (o no 😥) ya tienes un servidor apache corriendo y junto con el phpmyadmin. Pero para evitar problemas vamos a usar un contenedor de phpmyadmin. Para esto vamos a ejecutar el siguiente comando:

A día de hoy 6 de Julio de 2023 en la documentación oficial de [phpmyadmin](https://hub.docker.com/r/phpmyadmin/phpmyadmin) se menciona el uso de la flag `--link` para conectar el contenedor de phpmyadmin con el contenedor de mysql. Pero esta flag está deprecada desde la versión 1.13.0 de docker-compose. Por lo que vamos a usar el siguiente comando:

<kbd style="background-color: #CCFFCC;margin-bottom: 10px; padding: 10px; line-height: 1.5;">
<strong>Nota:</strong> Al ser una función legacy puede que en un futuro deje de funcionar. Por lo que no se debe usar. Fue sustituido por `--network`.
</kbd>

```bash
docker container run \
--name phpmyadmin \
-d \
-e PMA_ARBITRARY=1 \
-p 8080:80 \
phpmyadmin:5.2.0-apache
```
## Container Networking

Visitar la [documentación oficial](https://docs.docker.com/network/).

Para poder conectar el contenedor de phpmyadmin con el contenedor de mysql será necesario crear una red, para esto vamos a ejecutar el siguiente comando:
```bash
docker network create NOMBRE_RED
```

Posteriormente vamos a conectar los contenedores a la red que acabamos de crear. Para esto vamos a ejecutar el siguiente comando:
```bash
docker network connect NOMBRE_RED CONTAINER1_ID
docker network connect NOMBRE_RED CONTAINER2_ID
```

Para corroborar que los contenedores estén conectados a la red vamos a ejecutar el siguiente comando:
```bash
docker network inspect NOMBRE_RED
```

<kbd style="background-color: #CCFFCC;margin-bottom: 10px; padding: 10px; line-height: 1.5;">
  <strong>REGLA DE ORO:</strong> Si dos o más contenedores están en la misma red, podrán hablar entre sí. Si no lo están, no podrán.
</kbd>

- Ver comandos de networking: `docker network`
- Crear una nueva red: `docker network create NOMBRE_RED`
- Lista las redes: `docker network ls`

Recargamos la página de phpmyadmin y nos debería de dejar entrar. En el campo de servidor ponemos el nombre del contenedor de mysql `world-db` y en el usuario y contraseña los que definimos anteriormente.

Existe otra manera de poder designar la red a la hora de levantar el contenedor. Para esto instaleremos de nuevo los contenedores de mariadb y phpmyadmin. Recordemos que tenemos un volumen llamado `world-db` que contiene la data de la base de datos.

MariaDB:
```bash
docker container run \
--name world-db \
-dp 3306:3306 \
--env MYSQL_USER=admin \
--env MYSQL_PASSWORD=admin123 \
--env MYSQL_ROOT_PASSWORD=root123 \
--env MYSQL_DATABASE=world-db \
--volume world-db:/var/lib/mysql \
--network world-app \
mariadb:jammy
```

PhpMyAdmin:
```bash
docker container run \
--name phpmyadmin \
-d \
-e PMA_ARBITRARY=1 \
-p 8080:80 \
--network world-app \
phpmyadmin:5.2.0-apache
```

Ahora ya tenemos los contenedores conectados a la red `world-app`. Para corroborar esto vamos a ejecutar el siguiente comando:
```bash
docker network inspect world-app
```

## Docker Compose

Es una herramienta que se desarrolló para ayudar a definir y compartir aplicaciones de varios contenedores.

Para esto creamos el archivo `docker-compose.yml` con el siguiente contenido:
```yml
version: '3'

services:
  db: # Nombre del servicio
    container_name: postgres_database # Nombre del contenedor. Este nombre será el "hostname" del contenedor.
    image: postgres:15.1 # Imagen a usar
    volumes: # Volumen a usar. En este caso es un volumen anónimo.
      - postgres-db:/var/lib/postgresql/data
    environment:
      - POSTGRES_PASSWORD=123456 # Variables de entorno

  pgAdmin: # Nombre del servicio
    depends_on: # Dependencia del servicio
      - db # Nombre del servicio al que depende

    image: dpage/pgadmin4:6.17 # Imagen a usar
    ports: # Puerto a usar. Primer número es el puerto del host y el segundo es el puerto del contenedor.
      - "8080:80"
    environment:
      - PGADMIN_DEFAULT_PASSWORD=123456
      - PGADMIN_DEFAULT_EMAIL=superman@batman.com

volumes: # Se coloca postgres-db porque es el nombre del volumen que se está usando en el servicio db. Revisar con `docker volume ls`
  postgres-db:
```

<details>
  <summary>Comandos de docker-compose</summary>
  Si colocamos el siguiente comando nos mostrará los comandos de docker-compose:
  `docker compose --help`
  <br>
  <ul>
  <li>docker compose build: Construye los servicios.</li>
  <li>docker compose convert: Convierte el archivo docker-compose.yml a diferentes formatos.</li>
  <li>docker compose cp: Copia archivos entre el host y los contenedores.</li>
  <li>docker compose create: Crea los servicios.</li>
  <li>docker compose down: Detiene y elimina los servicios.</li>
  <li>docker compose events: Muestra los eventos de los servicios.</li>
  <li>docker compose exec: Ejecuta comandos en los servicios.</li>

<li>docker compose images: Lista las imágenes de los servicios.</li>
<li>docker compose kill: Detiene los servicios.</li>
<li>docker compose logs: Muestra los logs de los servicios.</li>
<li>docker compose ls: Lista los servicios.</li>
<li>docker compose pause: Pausa los servicios.</li>
<li>docker compose port: Muestra el puerto de los servicios.</li>
<li>docker compose ps: Lista los servicios.</li>
<li>docker compose pull: Descarga las imágenes de los servicios.</li>
<li>docker compose push: Sube las imágenes de los servicios.</li>
<li>docker compose restart: Reinicia los servicios.</li>
<li>docker compose rm: Elimina los servicios.</li>
<li>docker compose run: Ejecuta los servicios.</li>
<li>docker compose start: Inicia los servicios.</li>
<li>docker compose stop: Detiene los servicios.</li>
<li>docker compose top: Muestra los procesos de los servicios.</li>
<li>docker compose unpause: Reanuda los servicios.</li>
<li>docker compose up: Inicia los servicios.</li>
<li>docker compose version: Muestra la versión de docker-compose.</li>
</ul>
</details>

Una vez creado el archivo vamos a ejecutar el siguiente comando para levantar los contenedores:
```bash
docker compose up
```

Ese comando va a buscar el archivo `docker-compose.yml` y va a levantar los contenedores que se encuentren ahí. Es necesario estar en el mismo directorio donde se encuentra el archivo.

Lo que hace el comando es que crea una capa de múltiples contenedores que se pueden comunicar entre sí. Se puede ver visualmente docker desktop. El contenedor adopta el nombre de la carpeta del proyecto.

La nomenclatura de los contenedores usado en el docker compose:

`<project-name>_<service-name>_<replica-number>`

Una vez que se levanten los contenedores podremos ir a `localhost:8080` y nos debería de dejar entrar a pgadmin. Es importante mencionar que de momento no se le ha asignado ningún directorio para almacenar la información de la base de datos. Esto se le tiene que asignar manualmente. Aunque hay algunas cosas que hacer antes de volverlo a ejecutar. Lo primero sería cancelar ejecución del contenedor (en caso de no haberse ejecutado en modo detach) usando `ctrl + c`.

A continuación se debe realizar unos cambios en el archivo `docker-compose.yaml`

```yml

# código anterior

volumes:
  postgres-db: # Nombre del volumen externo. `docker volume ls`
    external: true
```

Si ahora se ejecuta el comando `docker compose up` no se verá el cambio reflejado ya que en este caso se necesita realizar una recreación de todos los contenedores. Es decir que tenemos que hacer una limpieza.

Existe un comando que nos va a permitir automatizar este proceso, básicamente lo que hace es lo mismo pero a la inversa.

`docker compose down`

Esto en alguna ocasiones suele dejar un poco de rastro (en cuestión de volúmenes). Eliminamos el volumen creado (si así fuere) con el siguiente comando: `docker volume rm <nombre del volumen>`

Ahora si ejecutamos de nuevo `docker compose up` nos debería de tomar el cambio de lo que hicimos en el archivo `docker-compose.yml`. Y tomar el volumen externo que le asignamos.

Ahora se mapea el lugar donde se graba la información, para eso se aplica un bind volume para que se guarde en el directorio local.

```yml
#version: '3'

#services:
  db: # Nombre del servicio
    container_name: postgres_database # Nombre del contenedor. Este nombre será el "hostname" del contenedor.
    image: postgres:15.1 # Imagen a usar
    volumes: # Volumen a usar. En este caso es un volumen anónimo.
      - ./dockerCurso:/var/lib/postgresql/data # Se mapea el directorio local con el directorio del contenedor. Se usa `./` para indicar que es el directorio actual.
    environment:
      - POSTGRES_PASSWORD=123456 # Variables de entorno

  pgAdmin: # Nombre del servicio
    depends_on: # Dependencia del servicio
      - db # Nombre del servicio al que depende

    image: dpage/pgadmin4:6.17 # Imagen a usar
    ports: # Puerto a usar. Primer número es el puerto del host y el segundo es el puerto del contenedor.
      - "8080:80"
    environment:
      - PGADMIN_DEFAULT_PASSWORD=123456
      - PGADMIN_DEFAULT_EMAIL=superman@batman.com

volumes: # Se coloca postgres-db porque es el nombre del volumen que se está usando en el servicio db. Revisar con `docker volume ls`
  postgres-db:
```

Para agregar pgAdmin sería:

```yml
  pgAdmin:
    depends_on:
      - db
    image: dpage/pgadmin4:6.17
    ports:
      - "8080:80"
    volumes:
      - ./pgadmin:/var/lib/pgadmin
    environment:
      - PGADMIN_DEFAULT_PASSWORD=123456
      - PGADMIN_DEFAULT_EMAIL=superman@batman.com
```

En caso de que aparezca este error:

![PermissionError](./Screenshot_2023-07-09_10-27-43.png)

Es un error de permisos lo podemos solucionar con change owner:
```bash
sudo mkdir -p /var/lib/pgadmin/sessions
sudo chown -R 5050:5050 /var/lib/pgadmin
```

Ese comando lo que hace es que le otorga los permisos necesarios al directorio de pgadmin.

Ahora podemos ejecutar `docker compose up -d`.

<kbd style="background-color: #CCFFCC;margin-bottom: 10px; padding: 10px; line-height: 1.5;">
<strong>Importante:</strong> Si se está usando un controlador de versiones como git es necesario incluir los directorios creados al archivo .gitignore para evitar posibles filtraciones.
</kbd>


## Práctica

Es importante practicar una y otra vez para generar la memoria muscular. Así que vamos a hacer otro ejercicio.

Para esta práctica vamos a necesitar:

- MongoDB
- Mongo Express
- [Pokemón nest app](https://hub.docker.com/r/klerith/pokemon-nest-app)


Lo primero va a ser crearnos una carpeta para el proyecto por ejemplo: `pokemon-app`.

```bash
`mkdir pokemon-app`
```

Creamos dos archivos:

- `touch .env docker-compose.yml`


Y colocamos los siguiente en el archivo `docker-compose.yml`:

```yml
version: '3'


services:
  mongoDb:
    container_name: pokemon_db
    image: mongo:6.0
    volumes:
      - poke-vol:/data/db


volumes:
  poke-vol:
    external: false
```

Con eso podríamos ya levantar el servicio de mongo y funcionaría sin problemas.

Pero queremos que tenga el servicio de autenticación para hacerla un poco más segura, para eso se usa `--auth` al momento de levantar el servicio. Revisar [documentación](https://hub.docker.com/_/mongo).

Dentro del archivo `docker-compose.yml` agregamos:
```yml
version: '3'


services:
  mongoDb:
    container_name: pokemon_db
    image: mongo:6.0
    volumes:
      - poke-vol:/data/db
    ports:
      - "27017:27017"
    restart: always
    environment:
      MONGO_INITDB_ROOT_USERNAME: mongoadmin
      MONGO_INITDB_ROOT_PASSWORD: 123456
    command: ["--auth"]


volumes:
  poke-vol:
    external: false
```

<kbd style="background-color: #CC222F; margin-bottom: 10px; padding: 10px; line-height: 1.5;">
<strong>Importante:</strong> En el archivo .env se colocan las variables de entorno que se van a usar en el archivo docker-compose.yml. El ejemplo de arriba es solo informativo y no se deben de colocar las contraseñas en ese archivo .yml.
</kbd>

Se debe de borrar el volumen creado anteriormente, para que funcione correctamente. `volume rm <nombre del volumen>`.

Ahora una vez eliminado el volumen, procedemos a levantar el contenedor. `docker compose up`

Nos conectará correctamente, ahora para conectarnos mediante la shell de mongo:

```bash
mongosh "mongodb://mongoadmin:123456@localhost:27017"
```

En el archivo `.env` colocamos las variables de entorno que se van a utilizar en el archivo `docker-compose.yml`:

Archivo `.env`:
```
MONGO_USERNAME=mongoadmin
MONGO_PASSWORD=123456789
MONGO_DB_NAME=pokemon_db
```

Archivo `docker-compose.yml`:
```yml

version: '3'


services:
  mongoDb:
    container_name: ${MONGO_DB_NAME}
    image: mongo:6.0
    volumes:
      - poke-vol:/data/db
    ports:
      - "27017:27017"
    restart: always
    environment:
      MONGO_INITDB_ROOT_USERNAME: ${MONGO_USERNAME}
      MONGO_INITDB_ROOT_PASSWORD: ${MONGO_PASSWORD}
    command: ["--auth"]


volumes:
  poke-vol:
    external: false

 ```

 Ahora podemos levantar el contenedor con `docker compose up -d` y nos conectamos con la shell de mongo con:
```bash
mongosh "mongodb://mongoadmin:123456@localhost:27017"
```

Y listo ya tenemos un contenedor de mongo con autenticación.

<kbd style="background-color: #CC222F;margin-bottom: 10px; padding: 10px; line-height: 1.5;">
<strong>Importante:</strong> Es importante que al momento de levantar el contenedor se vea en los logs que se creo el volumen, así garantizamos que no se va a estar usando ningún otro.
</kbd>

Ahora podemos continuar con las siguientes dependencias.

Nuestro archivo `docker-compose.yml` quedaría de la siguiente forma:

```yml

version: '3'

services:
  mongoDb:
    container_name: ${MONGO_DB_NAME}
    image: mongo:6.0
    volumes:
      - poke-vol:/data/db
    ports:
      - "27017:27017"
    restart: always
    environment:
      MONGO_INITDB_ROOT_USERNAME: ${MONGO_USERNAME}
      MONGO_INITDB_ROOT_PASSWORD: ${MONGO_PASSWORD}
    command: [ "--auth" ]
  mongo-express:
    depends_on:
      - mongoDb
    image: mongo-express:1.0.0-alpha.4
    environment:
      ME_CONFIG_MONGODB_ADMINUSERNAME: ${MONGO_USERNAME}
      ME_CONFIG_MONGODB_ADMINPASSWORD: ${MONGO_PASSWORD}
      ME_CONFIG_MONGODB_SERVER: ${MONGO_DB_NAME}
    ports:
      - "8080:8081"

    restart: always

volumes:
  poke-vol:
    external: false
```

Ahora levantamos el contenedor con `docker compose up -d` y nos conectamos a `localhost:8080` y nos aparecerá la página de inicio de `Mongo Express`.

Ya estaría conectado, pero recordemos que una de las cosas que viene a implementar docker es el "*Aislamiento*". Así que no hay necesidad de exponer el puerto local del servicio de mongo. Así que vamos a quitar el puerto `27017` del servicio de mongo.
```yml

version: '3'

services:
  mongoDb:
    container_name: ${MONGO_DB_NAME}
    image: mongo:6.0
    volumes:
      - poke-vol:/data/db
    restart: always
    environment:
      MONGO_INITDB_ROOT_USERNAME: ${MONGO_USERNAME}
      MONGO_INITDB_ROOT_PASSWORD: ${MONGO_PASSWORD}
    command: [ "--auth" ]
  mongo-express:
    depends_on:
      - mongoDb
    image: mongo-express:1.0.0-alpha.4
    environment:
      ME_CONFIG_MONGODB_ADMINUSERNAME: ${MONGO_USERNAME}
      ME_CONFIG_MONGODB_ADMINPASSWORD: ${MONGO_PASSWORD}
      ME_CONFIG_MONGODB_SERVER: ${MONGO_DB_NAME}
    ports:
      - "8080:8081"

    restart: always

volumes:
  poke-vol:
    external: false
```

Levantamos el contenedor con `docker compose up -d` y nos conectamos a `localhost:8080` y nos aparecerá la página de inicio de `Mongo Express`. Sin embargo si tratamos de conectarnos como hace un momento mediante la mongo shell, no nos dejará, ya que no expusimos el puerto, solamente lo puede ver el contenedor.

Por último, se agrega la imagen de [pokemon-nest-app](https://hub.docker.com/r/klerith/pokemon-nest-app) en el archivo `docker-compose.yml`:
```yml
version: '3'

services:
  mongoDb:
    container_name: ${MONGO_DB_NAME}
    image: mongo:6.0
    volumes:
      - poke-vol:/data/db
      #ports:
      #  - "27017:27017"
    restart: always
    environment:
      MONGO_INITDB_ROOT_USERNAME: ${MONGO_USERNAME}
      MONGO_INITDB_ROOT_PASSWORD: ${MONGO_PASSWORD}
    command: [ "--auth" ]
  mongo-express:
    depends_on:
      - mongoDb
    image: mongo-express:1.0.0-alpha.4
    environment:
      ME_CONFIG_MONGODB_ADMINUSERNAME: ${MONGO_USERNAME}
      ME_CONFIG_MONGODB_ADMINPASSWORD: ${MONGO_PASSWORD}
      ME_CONFIG_MONGODB_SERVER: ${MONGO_DB_NAME}
    ports:
      - "8080:8081"

    restart: always

  poke-app:
    depends_on:
      - mongoDb
      - mongo-express
    image: klerith/pokemon-nest-app:1.0.0
    ports:
      - "3000:3000"
    environment:
      MONGODB: mongodb://${MONGO_USERNAME}:${MONGO_PASSWORD}@${MONGO_DB_NAME}:27017
      DB_NAME: ${MONGO_DB_NAME}
    restart: always

volumes:
  poke-vol:
    external: false
```


## Creación de la imagen 

Al ejecutar `docker buildx ls` nos mostrará los *builders* que tenemos disponibles, en este caso solo tenemos el builder por defecto, el cual es `docker-container`:

En un archivo `Dockerfile` el orden de cada comando es importante, especialmente si se quiere manejar correctamente el caché de las capas.

- **Herencia de imágenes:** Este paso basa nuestra imagen a crear, partir de otra en particular.
```dockerfile
FROM node:18.3.1
```

- **Asignar alias (Multi-State):** Se asigna un alias a esta etapa llamada: "builder", la cual permite realizar un multi-stage build
```dockerfile
FROM node:18.3.1 AS builder
```

- **Especificar la plataforma:** Útil para M1/M2, ya que permite especificar la plataforma a la cual se va a construir la imagen.
```dockerfile
FROM --platform=linux/amd64 node:18-alpine
```

- **Variables y uso:** Se crea una variable llamada APP_HOME con el valor de "/app"
```dockerfile
ENV APP_HOME /app
RUN mkdir $APP_HOME
```

- **Inicialización:** Se indica que se deben de descargar e instalar los módulos de node.
```dockerfile
RUN npm install
RUN yarn install --frozen-lockfile
```

- **Workdir:** Establecer que partir de este punto, estamos en el directorio especificado, es como cambiarse de directorio vía comando.
```dockerfile
WORKDIR /app
```

- **Punto de montaje:** Se establece el punto de montaje para el volumen. Este punto de montaje se asignará a una ubicación en el host que se especifica cuando se crea el contenedor o, si no se especifica, se elige automáticamente desde un directorio creado en `/var/lib/docker/volumes`
```dockerfile
VOLUME ["/data"]
```

- **Copia todos los archivos:** Copia todos los archivos del directorio actual al directorio especificado en el contenedor. Excluye los archivos y directorios que se encuentran en el archivo `.dockerignore`
```dockerfile
COPY ..
```
- **Expose:** Expone el puerto 3000 del contenedor Informa a Docker que el contenedor escucha en los puerto de red especificado en tiempo de ejecución.
```dockerfile
EXPOSE 3000
```

- **Comando:** Ejecuta el comando especificado dentro del contenedor. Son instrucciones que se ejecutarán cuando se inicie un contenedor Docker.
```dockerfile
CMD [ "node", "dist/main"]
```

Se considera una **buena práctica** reconstruir las imágenes de Docker periódicamente para garantizar que se apliquen las actualizaciones de seguridad más recientes y que se utilicen las versiones más recientes de las imágenes base.
`docker build --no-cache -t <image-name>:<tag> .`


El archivo `Dockerfile` contiene las instrucciones para construir la imagen, en este caso se va a crear una imagen de la aplicación de nestjs, la cual se encuentra en el repositorio [pokemon-nest-app](

Como se menciona en el [Glosario de términos](#glosario-de-términos), una imagen es un archivo de solo lectura que contiene un conjunto de capas que representan instrucciones para crear un contenedor. 



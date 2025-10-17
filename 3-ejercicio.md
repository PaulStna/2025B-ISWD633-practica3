## Esquema para el ejercicio
![Imagen](esquema-ejercicio3.PNG)

### Crear red net-wp
```
docker network create net-wp -d bridge
```

### Para que persista la información es necesario conocer en dónde mysql almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio carpeta del contenedor (a) es **/var/lib/mysql**

Ruta carpeta host: .../ejercicio3/db

### ¿Qué contiene la carpeta db del host?
Inicialmente la carpeta db del host está vacía.

### Crear un contenedor con la imagen mysql:8  en la red net-wp, configurar las variables de entorno: MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, MYSQL_USER y MYSQL_PASSWORD
```
docker run -d --name mysql-service --network net-wp -v "D:\Documentos\ESCUELA POLITECNICA NACIONAL\6to Semestre\Construccion y Evolucion de Software\Practicas\2025B-ISWD633-practica3\nginx\ejercicio3\db":/var/lib/mysql -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=wordpress -e MYSQL_USER=wpuser -e MYSQL_PASSWORD=wppass mysql:8
```

### ¿Qué observa en la carpeta db que se encontraba inicialmente vacía?
La carpeta db del host, que al inicio estaba vacía, ahora contiene los archivos y directorios del sistema de base de datos (por ejemplo, datos, logs y configuraciones internas).

### Para que persista la información es necesario conocer en dónde wordpress almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio la carpeta del contenedor (b) es **/var/www/html**

Ruta carpeta host: .../ejercicio3/www

### Crear un contenedor con la imagen wordpress en la red net-wp, configurar las variables de entorno WORDPRESS_DB_HOST, WORDPRESS_DB_USER, WORDPRESS_DB_PASSWORD y WORDPRESS_DB_NAME (los valores de estas variables corresponden a los del contenedor creado previamente)
```
docker run -d --name wordpress --network net-wp -v "D:\Documentos\ESCUELA POLITECNICA NACIONAL\6to Semestre\Construccion y Evolucion de Software\Practicas\2025B-ISWD633-practica3\nginx\ejercicio3\www":/var/www/html -e WORDPRESS_DB_HOST=mysql-service:3306 -e WORDPRESS_DB_USER=wpuser -e WORDPRESS_DB_PASSWORD=wppass -e WORDPRESS_DB_NAME=wordpress -p 9500:80 wordpress
```

### Personalizar la apariencia de wordpress y agregar una entrada

### Eliminar el contenedor y crearlo nuevamente, ¿qué ha sucedido?
Al recrear el contenedor de WordPress con volúmenes, tanto la base de datos como los archivos de temas, plugins y entradas se conservan, por lo que el sitio mantiene su contenido y apariencia sin perder datos o configuraciones.

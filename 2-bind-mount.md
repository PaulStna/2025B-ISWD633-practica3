# BIND MOUNT
En un bind mount mapeamos (montar) un directorio o archivo específico del sistema de archivos del host con una parte del sistema de ficheros del contenedor.

```
docker run -d --name <nombre contenedor> -v <ruta carpeta host>:<ruta carpeta contenedor> <imagen> 
```
ó
```
docker run -d --name <nombre contenedor> --mount type=bind,source=<ruta carpeta host>,target=<ruta carpeta contenedor> <imagen>
```
- destination, dst, target: La ruta donde se monta el archivo o directorio en el contenedor.
- source, src: El origen del montaje.
  
### En tu computador crear una carpeta llamada nginx y dentro de esta carpeta crea otra llamada html. Como se aprecia en la figura.
![Volúmenes](directorio.PNG)

### Crear un contenedor con la imagen nginx:alpine, mapear todos por puertos, para la ruta carpeta host colocar el directorio en donde se encuentra la carpeta html en tu computador y para la ruta carpeta contenedor: /usr/share/nginx/html (esta ruta se obtiene al revisar la documentación de la imagen)
![Volúmenes](volumen-host.PNG)
```
docker run -d --name nginx-server -p 8080:80 -v "D:\Documentos\ESCUELA POLITECNICA NACIONAL\6to Semestre\Construccion y Evolucion de Software\Practicas\2025B-ISWD633-practica3\nginx\html":/usr/share/nginx/html nginx:alpine
```

### ¿Qué sucede al ingresar al servidor de nginx?
Aparece el mensaje “403 Forbidden”, porque Nginx intenta acceder al directorio montado desde el host, pero no encuentra ningún archivo index.html para mostrar.

### ¿Qué pasa con el archivo index.html del contenedor?
El archivo index.html original que viene dentro del contenedor de Nginx es reemplazado temporalmente por el volumen montado desde el host.
Por ello, si la carpeta del host está vacía, Nginx no puede acceder a su propio index.html y muestra el error 403 Forbidden.

### Ir a https://html5up.net/ y descargar un template gratuito, descomprirlo dentro de tu computador en la carpeta html
### ¿Qué sucede al ingresar al servidor de nginx?
Al ingresar nuevamente al servidor, Nginx muestra correctamente el sitio del template HTML descargado, ya que ahora existe un archivo index.html dentro del volumen montado.

### Eliminar el contenedor
```
docker rm -f nginx-server
```

### ¿Qué sucede al crear nuevamente un contenedor montado al directorio definidos anteriormente?
Después de eliminar el contendor y crearlo nuevamente con el mismo volumen montado, Nginx vuelve a mostrar el sitio web del template que se encuentra en la carpeta local.
Esto ocurre porque los archivos permanecen en el host, por lo que aunque se elimine y recree el contenedor, el contenido HTML sigue disponible y se sirve correctamente desde la misma ruta.


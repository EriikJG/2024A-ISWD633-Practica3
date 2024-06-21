# VOLUMEN TIPO HOST
Un volumen host (o bind mount) es un tipo de volumen donde se monta un directorio o archivo específico del sistema de archivos del host en un contenedor.

```
docker run -d --name <nombre contenedor> -v <ruta carpeta host>:<ruta carpeta contenedor> <imagen> 
```

### Crear un volumen tipo host con la imagen nginx:alpine, para la ruta carpeta host: directorio en donde se encuentra la carpeta html en tu computador y para la ruta carpeta contenedor: /usr/share/nginx/html esta ruta se obtiene al revisar la documentación
![Volúmenes](imagenes/volumen-host.PNG)
```
docker run -d --name nginx1 -p 8080:80 -v //c/Users/LabP3E010/Documents/html:/usr/share/nginx/html nginx:alpine
```
### ¿Qué sucede al ingresar al servidor de nginx?
*Ocurre un error 403*

### ¿Qué pasa con el archivo index.html del contenedor?
*El archivo index.html del contenedor no es accesible porque el usuario que ejecuta Nginx no tiene permisos para leer el contenido del directorio /usr/share/nginx/html. 
El error 403 indica que el servidor Nginx tiene acceso al directorio, pero no puede leer el contenido debido a restricciones de permisos.*

### Ir a https://html5up.net/ y descargar un template gratuito, descomprirlo dentro de nginx/html
### ¿Qué sucede al ingresar al servidor de nginx?
*Se carga el template gratuito que descargue.*

### Eliminar el contenedor
```
docker rm -f nginx1
```
### ¿Qué sucede al crear nuevamente el mismo contenedor con volumen de tipo host a los directorios definidos anteriormente?
*Se carga el template y ya no ocurre el error 403.*

### ¿Qué hace el comando pwd?

*pwd imprime la ruta absoluta del directorio en el que se encuentra el usuario en ese momento. Esto puede ser útil para saber dónde se encuentra actualmente en el sistema de archivos.*

### Volumen tipo host usando PWD y PowerShell
```
docker run -d --name <nombre contenedor> --publish published=<valorPuertoHost>,target=<valor> -v ${PWD}/<ruta relativa>:<ruta absoluta> <nombre imagen>:<tag> 
```

### Volumen tipo host usando PWD (Git Bash)

```
docker run -d --name <nombre contenedor> --publish published=<valorPuertoHost>,target=<valor> -v $(pwd -W)/html:/usr/share/nginx/html <nombre imagen>:<tag> 
```

### Volumen tipo host usando PWD (en Linux)

```
docker run -d --name <nombre contenedor> --publish published=<valorPuertoHost>,target=<valor> -v $(pwd)/html:/usr/share/nginx/html <nombre imagen>:<tag> 
```


## Esquema para el ejercicio
![Imagen](imagenes/esquema-ejercicio3.PNG)

### Crear red net-wp
```
docker network create net-wp
```

### Para que persista la información es necesario conocer en dónde mysql almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/)
En el esquema del ejercicio la carpeta contenedor (a) es /var/lib/mysql.
Ruta carpeta host: .../ejercicio3/db

### ¿Qué contiene la carpeta db del host?
Contiene los datos de la base de datos de MySQL.

### Crear un contenedor con la imagen mysql:8  en la red net-wp, configurar las variables de entorno: MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, MYSQL_USER y MYSQL_PASSWORD
```
docker run -d --name mysql-container --network net-wp -p 3306:3306 -v //c/Users/LabP3E010/Documents/db:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root_password -e MYSQL_DATABASE=wordpress_db -e MYSQL_USER=wp_user -e MYSQL_PASSWORD=wp_password mysql:8

```

### ¿Qué observa en la carpeta db que se encontraba inicialmente vacía?
Ahora contiene los archivos y directorios de datos utilizados por MySQL para almacenar la información de la base de datos.

### Para que persista la información es necesario conocer en dónde wordpress almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio, la carpeta contenedor (b) es /var/www/html.
Ruta carpeta host: ../ejercicio3/www

### Crear un contenedor con la imagen wordpress en la red net-wp, configurar las variables de entorno WORDPRESS_DB_HOST, WORDPRESS_DB_USER, WORDPRESS_DB_PASSWORD y WORDPRESS_DB_NAME (los valores de estas variables corresponden a los del contenedor creado previamente)

```
docker run -d --name wordpress-container --network net-wp -p 9500:80 -v //c/Users/LabP3E010/Documents/www:/var/www/html -e WORDPRESS_DB_HOST=mysql-container -e WORDPRESS_DB_USER=wp_user -e WORDPRESS_DB_PASSWORD=wp_password -e WORDPRESS_DB_NAME=wordpress_db wordpress

```

### Personalizar la apariencia de wordpress y agregar una entrada

### Eliminar el contenedor y crearlo nuevamente, ¿qué ha sucedido?

Cuando vuelves a crear el contenedor wordpress-container, la personalización y las entradas que hayas agregado previamente en WordPress deberían persistir. Esto ocurre porque el volumen montado (//c/Users/LabP3E010/Documents/www) contiene todos los datos y configuraciones de WordPress. El contenedor simplemente vuelve a utilizar estos datos al ser creado de nuevo.



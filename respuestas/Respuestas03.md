# Imagenes, Volumenes y Redes
---
## Ejercicios prácticos

### Ejercicio 1: Persistencia con volúmenes

Crear volumen y contenedor MySQL
```bash
docker volume create vol_mysql
docker run -d --name mysql-test -e MYSQL_ROOT_PASSWORD=1234 \
  -v vol_mysql:/var/lib/mysql mysql:8
```

Esperar a que MySQL inicialice, luego crear datos
```bash
docker exec -it mysql-test mysql -u root -p 1234 -e \
  "CREATE DATABASE demo; USE demo; \
   CREATE TABLE t(id INT); INSERT INTO t VALUES (1);"
```

Eliminar el contenedor (el volumen persiste)
```bash
docker rm -f mysql-test
```

Crear un contenedor nuevo apuntando al mismo volumen
```bash
docker run -d --name mysql-test2 -e MYSQL_ROOT_PASSWORD=1234 \
  -v vol_mysql:/var/lib/mysql mysql:8
```

Verificar que los datos siguen ahí
```bash
docker exec -it mysql-test2 mysql -uroot -p1234 -e "SELECT * FROM demo.t;"
```

**Explicación esperada:** *el volumen vol_mysql es un objeto independiente del ciclo de vida de cualquier contenedor específico; al eliminar el contenedor solo se destruye su capa de escritura y metadatos, no los datos almacenados en el volumen, que Docker gestiona por separado en el host.*

---

### Ejercicio 2: Bind mount para desarrollo

```bash
mkdir -p sitio && echo "<h1>Versión 1</h1>" > sitio/index.html

docker run -d --name web-bind -p 8082:80 \
  -v $(pwd)/sitio:/usr/share/nginx/html nginx
```
Modificar `sitio/index.html` a `<h1>Versión 2</h1>` y recargar el navegador: el cambio se refleja de inmediato porque el archivo real que Nginx sirve es el del host, montado directamente dentro del contenedor.

**Diferencia clave a documentar:**

- **Bind mount:** ruta gestionada por el usuario en el host, ideal para desarrollo (edición en vivo).
- **Volumen Docker:** ruta gestionada por Docker, ideal para persistencia de datos generados por el propio contenedor (bases de datos), más portable entre hosts.

---

### Ejercicio 3: PHP + MySQL en red personalizada

Comandos docker:

```bash
docker network create red-ej3
docker volume create vol_mysql_ej3

docker run -d --name db --network red-ej3 \
  -e MYSQL_ROOT_PASSWORD=secreto -e MYSQL_DATABASE=demo \
  -v vol_mysql_ej3:/var/lib/mysql mysql:8

docker run -d --name app --network red-ej3 -p 8083:80 \
  -v $(pwd)/src:/var/www/html php:8.2-apache
```

`src/index.php`

```bash
<?php
$conn = mysqli_connect('db', 'root', 'secreto', 'demo');
if ($conn) {
    echo "Conexión exitosa a MySQL desde PHP";
} else {
    echo "Error: " . mysqli_connect_error();
}
?>
```

**Explicación esperada:** *al estar ambos contenedores en la red red-ej3 (definida por el usuario), Docker resuelve automáticamente el nombre db a la IP interna del contenedor MySQL mediante su servidor DNS embebido, sin necesidad de conocer o fijar direcciones IP manualmente.*


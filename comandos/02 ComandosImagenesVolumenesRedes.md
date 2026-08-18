# Comandos: Imagenes, Volumenes y Redes

---

## Imagenes

| Comando | Descripción | Ejemplo |
|---------|-------------|---------|
| **`docker images`** o **`docker images ls`** | Lista las imágenes locales. | **`docker images`** o **`docker images ls`**  |
| **`docker pull`** | Descarga una imagen desde un Registry. | **`docker pull nginx`** |
| **`docker image inspect`** | Muestra información detallada de una imagen. | **`docker image inspect nginx`** |
| **`docker rmi`** | Elimina una imagen local. | **`docker rmi nginx`** |

---

## Volumenes

| Comando | Descripción | Ejemplo |
|---------|-------------|---------|
| **`docker volume ls`** | Lista los volúmenes. | **`docker volume ls`**  |
| **`docker volume create`** | Crea un nuevo volumen. | **`docker volume create datos-mysql`** |
| **`docker volume inspect`** | Muestra información detallada de un volumen. | **`docker volume inspect datos-mysql`** |
| **`docker volume rm `** | Elimina un volumen. | **`docker volume rm datos-mysql`** |

***`Nota: eliminar un volumen puede provocar pérdida de datos.`***

---

## Redes

| Comando | Descripción | Ejemplo |
|---------|-------------|---------|
| **`docker network ls`** | Lista las redes. | **`docker network ls`** |
| **`docker network create`** | Crea una red personalizada. | **`docker network create red-app`** |
| **`docker network inspect`** | Muestra información detallada de una red. | **`docker network inspect red-app`** |
| **`docker network connect`** | Conecta un contenedor a una red. | **`docker network connect red-app servidor-web`** |
| **`docker network disconnect`** | Desconecta un contenedor. | **`docker network disconnect red-app servidor-web`** |

---

## Ejemplo

Conectar un contenedor PHP y uno MySQL mediante una red Docker personalizada:
1. Crear la red
```bash
docker network create red-app
```

2. Levantar MySQL en esa red, con volumen para persistencia
```bash
docker volume create datos_mysql
docker run -d --name db --network red-app \
  -e MYSQL_ROOT_PASSWORD=secreto -e MYSQL_DATABASE=demo \
  -v datos_mysql:/var/lib/mysql mysql:8
```

3. Levantar PHP en la misma red, publicando el puerto 8000
```bash
docker run -d --name app --network red-app -p 8000:80 \
  -v $(pwd)/src:/var/www/html php:8.2-apache
```

4. Desde dentro del contenedor 'app', probar la resolución DNS hacia 'db'
```bash
docker exec -it app bash
  getent hosts db
  php -r "var_dump(mysqli_connect('db','root','secreto','demo'));"
```

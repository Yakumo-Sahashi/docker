# Docker

---

## Comandos Docker

| Comando | Descripción |
|---------|-------------|
| **`docker version`** | Muestra la versión del cliente y del servidor (daemon). |
| **`docker info`**	| Muestra información detallada del entorno Docker: contenedores, imágenes, driver de almacenamiento, recursos.|
| **`docker run`** | Crea y arranca un contenedor a partir de una imagen.|
| **`docker ps`** | Lista los contenedores en ejecución (usar -a para ver todos, incluidos detenidos).|
| **`docker start`** | Inicia un contenedor previamente detenido.|
| **`docker stop`** | Detiene un contenedor en ejecución de forma ordenada (SIGTERM, luego SIGKILL).|
| **`docker restart`** |Reinicia un contenedor|
| **`docker rm`** | Elimina uno o más contenedores detenidos.|
| **`docker exec`** | Ejecuta un comando dentro de un contenedor en ejecución (por ejemplo, abrir una shell).|
| **`docker logs`** | Muestra la salida estándar  generada por el contenedor.|


---

## Ejemplo 1

1. Verificar que Docker está instalado y corriendo
```bash
docker --version
docker info
```

2. Ejecutar el contenedor de bienvenida
```bash
docker run hello-world
```

3. Ejecutar un servidor web Nginx en segundo plano
```bash
docker run -d --name mi-nginx -p 8080:80 nginx
```

4. Verificar que el contenedor está corriendo
```bash
docker ps
```

5. Acceder desde el navegador a `http://localhost:8080`

6. Detener y eliminar el contenedor
```bash
docker stop mi-nginx
docker rm mi-nginx
```

---

## Ejemplo 2

Levantar un servidor Nginx, explorar su ciclo de vida y publicar su puerto:

1. Crear y ejecutar el contenedor en segundo plano, publicando el puerto `80 - 8080`
```bash
docker run -d --name web-demo -p 8080:80 nginx:latest
```

2. Listar contenedores activos
```bash
docker ps
```

3. Entrar a una shell dentro del contenedor
```bash
docker exec -it web-demo bash
  cat /etc/nginx/nginx.conf
  exit
```

4. Ver logs en tiempo real
```bash
docker logs -f web-demo
```

5. Detener, reiniciar y finalmente eliminar
```bash
docker stop web-demo
docker start web-demo
docker restart web-demo
docker stop web-demo && docker rm web-demo
```


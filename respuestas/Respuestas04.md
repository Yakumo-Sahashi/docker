# Docker Compose
---
## Ejercicios prácticos

### Ejercicio 1: Primer compose.yml

```yaml
services:
  web:
    image: nginx:latest
    ports:
      - "8090:80"
    networks:
      - red-propia

  cache:
    image: redis:latest
    networks:
      - red-propia

networks:
  red-propia:
```

```bash
docker compose up -d
docker compose ps
```

**Explicación esperada:** para comunicarse, `web` podría alcanzar a `cache` usando el hostname `cache` en el puerto `6379` (por ejemplo, desde una aplicación dentro del contenedor `web` que usara un cliente Redis), gracias a que Compose los coloca en la misma red y resuelve nombres de servicio automáticamente.

---

### Ejercicio 2: Variables de entorno con `.env`

`.env`:
```
NGINX_PORT=8091
PROJECT_NAME=demo-compose
```

`.env.example`:
```
NGINX_PORT=
PROJECT_NAME=
```

`compose.yml`:
```yaml
services:
  web:
    image: nginx:latest
    container_name: ${PROJECT_NAME}-web
    ports:
      - "${NGINX_PORT}:80"
```

```bash
docker compose up -d
docker compose ps    # el nombre y el puerto deben reflejar los valores del .env
```

---

### Ejercicio 3: Réplica del stack PHP + MySQL

`.env`:
```
DB_NAME=demo
DB_ROOT_PASSWORD=secreto123
```

`compose.yml`:
```yaml
services:
  web:
    image: nginx:latest
    ports:
      - "8092:80"
    volumes:
      - ./nginx/default.conf:/etc/nginx/conf.d/default.conf:ro
    depends_on:
      - app
    networks:
      - red-app

  app:
    image: php:8.2-fpm
    volumes:
      - ./src:/var/www/html
    environment:
      - DB_HOST=db
      - DB_NAME=${DB_NAME}
    networks:
      - red-app

  db:
    image: mysql:8
    environment:
      - MYSQL_ROOT_PASSWORD=${DB_ROOT_PASSWORD}
      - MYSQL_DATABASE=${DB_NAME}
    volumes:
      - datos_mysql:/var/lib/mysql
    networks:
      - red-app

volumes:
  datos_mysql:

networks:
  red-app:
```

```bash
docker compose up -d
docker compose down          # sin -v: el volumen datos_mysql se conserva
docker compose up -d         # los datos siguen presentes al volver a levantar
```

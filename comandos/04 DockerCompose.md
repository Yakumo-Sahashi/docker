# Comandos: Docker Compose

---

| Comando | Descripción | Ejemplo |
|---------|-------------|---------|
| **`docker compose up`** | Crea y levanta todos los servicios definidos en el archivo compose.yml. | **`docker compose up`**  |
| **`docker compose up -d`** | Igual que el anterior, pero en segundo plano (detached). | **`docker compose up -d`**  |
| **`docker compose down`** | Detiene y elimina los contenedores, redes creadas (los volúmenes se conservan salvo que se use -v). | **`docker compose down`**  |
| **`docker compose ps`** | Lista el estado de los servicios del proyecto actual. | **`docker compose ps`**  |
| **`docker compose logs`** | Muestra los logs combinados de todos los servicios (usar -f para seguirlos en vivo). | **`docker compose logs`**  |
| **`docker compose restart`** | Reinicia uno o todos los servicios del proyecto. | **`docker compose restart`**  |

---

## Ejemplo

Construir la pila Nginx → PHP → MySQL completa y levantarla con un solo comando:

archivo *`Dockerfike`*

```bash

```

archivo *`compose.yaml`*

```
services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"
    volumes:
      - ./nginx.conf:/etc/nginx/conf.d/default.conf:ro
    depends_on:
      - app
    networks:
      - red-app

  app:
    build: ./app
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
docker compose ps
docker compose logs -f app
```
Verificar en el navegador: *http://localhost:8080*

Apagar todo el entorno
```bash
docker compose down
```
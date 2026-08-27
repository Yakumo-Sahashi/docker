# Proyecto Integrador

---
## Solución de referencia

Estructura de archivos:

```
proyecto-integrador/
├── docker-compose.yml
├── .env
├── .env.example
├── nginx/
│   └── default.conf
└── app/
    ├── Dockerfile
    ├── .dockerignore
    └── (código fuente de Laravel)
```

**`.env.example`:**
```
DB_DATABASE=laravel
DB_USERNAME=laravel_user
DB_PASSWORD=cambia_esta_clave
DB_ROOT_PASSWORD=cambia_esta_clave_root
APP_PORT=8080
```

**`app/Dockerfile`:**
```dockerfile
FROM composer:2 AS vendor
WORKDIR /app
COPY composer.json composer.lock ./
RUN composer install --no-dev --optimize-autoloader --no-scripts

FROM php:8.2-fpm
RUN apt-get update && apt-get install -y libzip-dev unzip \
    && docker-php-ext-install pdo_mysql zip \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /var/www/html
COPY --from=vendor /app/vendor ./vendor
COPY . .

RUN useradd -m appuser && chown -R appuser:appuser /var/www/html
USER appuser

EXPOSE 9000
```

**`app/.dockerignore`:**
```
.git
node_modules
tests
*.md
.env
```

**`nginx/default.conf`:**
```nginx
server {
    listen 80;
    index index.php;
    root /var/www/html/public;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        fastcgi_pass app:9000;
        fastcgi_index index.php;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }
}
```

**`docker-compose.yml`:**
```yaml
services:
  web:
    image: nginx:latest
    ports:
      - "${APP_PORT}:80"
    volumes:
      - ./nginx/default.conf:/etc/nginx/conf.d/default.conf:ro
      - ./app:/var/www/html:ro
    depends_on:
      - app
    networks:
      - red-proyecto

  app:
    build: ./app
    environment:
      - DB_CONNECTION=mysql
      - DB_HOST=db
      - DB_DATABASE=${DB_DATABASE}
      - DB_USERNAME=${DB_USERNAME}
      - DB_PASSWORD=${DB_PASSWORD}
    volumes:
      - ./app:/var/www/html
    depends_on:
      - db
    networks:
      - red-proyecto

  db:
    image: mysql:8
    environment:
      - MYSQL_DATABASE=${DB_DATABASE}
      - MYSQL_USER=${DB_USERNAME}
      - MYSQL_PASSWORD=${DB_PASSWORD}
      - MYSQL_ROOT_PASSWORD=${DB_ROOT_PASSWORD}
    volumes:
      - datos_mysql:/var/lib/mysql
    networks:
      - red-proyecto

volumes:
  datos_mysql:

networks:
  red-proyecto:
```

**Levantamiento y verificación:**
```bash
docker compose up -d --build
docker compose ps
# Verificar en http://localhost:8080
docker compose logs -f app
```

**Generación y distribución de la imagen final:**
```bash
docker build -t mi-laravel-app:1.0 ./app
docker tag mi-laravel-app:1.0 miusuario/mi-laravel-app:1.0
docker login
docker push miusuario/mi-laravel-app:1.0

# Desde otro equipo/entorno:
docker pull miusuario/mi-laravel-app:1.0
```

**Checklist de cumplimiento (según rúbrica):**
- [x] Tres servicios conectados por red propia (`red-proyecto`), con `depends_on` declarado.
- [x] Dockerfile con multi-stage build, capas ordenadas, `.dockerignore`, usuario no root.
- [x] Volumen `datos_mysql` persistente; credenciales parametrizadas vía `.env`.
- [x] Aplicación accesible en `http://localhost:8080`, conectando correctamente a MySQL.
- [x] Imagen publicada y verificada en un entorno distinto al original.

# Dockerfile, Imágenes Personalizadas y Proxy Inverso
---
## Ejercicios prácticos

### Ejercicio 1: Dockerfile básico para PHP

`Dockerfile`:
```dockerfile
FROM php:8.2-apache
COPY src/ /var/www/html/
EXPOSE 80
```

`src/index.php`:
```php
<?php phpinfo(); ?>
```

```bash
docker build -t practica-php:1.0 .
docker run -d --name php-ej1 -p 8093:80 practica-php:1.0
# Verificar en http://localhost:8093
```

---

### Ejercicio 2: Optimización de capas

`.dockerignore`:
```
.git
*.md
Dockerfile
.dockerignore
```

`Dockerfile` optimizado (mismo caso, con orden por frecuencia de cambio):
```dockerfile
FROM php:8.2-apache

# Capa poco cambiante: no hay dependencias de sistema extra en este ejemplo,
# pero si las hubiera irían aquí primero, por ejemplo:
# RUN apt-get update && apt-get install -y libzip-dev && rm -rf /var/lib/apt/lists/*

WORKDIR /var/www/html

# Código fuente al final: es lo que cambia con más frecuencia
COPY src/ .
EXPOSE 80
```

```bash
docker build -t practica-php:1.0 .     # build 1: construye todas las capas
# modificar únicamente src/index.php
docker build -t practica-php:1.0 .     # build 2: reutiliza la capa base (FROM) desde caché,
                                        # solo reconstruye desde el COPY en adelante
```

**Evidencia a documentar:** en la salida del segundo build, las capas anteriores al `COPY` deben mostrar `CACHED`, mientras que `COPY` y las instrucciones posteriores se reconstruyen.

---

### Ejercicio 3: Nginx como proxy inverso

`nginx/default.conf`:
```nginx
server {
    listen 80;

    location / {
        fastcgi_pass app:9000;
        fastcgi_index index.php;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME /var/www/html$fastcgi_script_name;
    }
}
```

```bash
docker network create red-ej3-m5

docker run -d --name app --network red-ej3-m5 \
  -v $(pwd)/src:/var/www/html php:8.2-fpm

docker run -d --name proxy --network red-ej3-m5 -p 8094:80 \
  -v $(pwd)/nginx/default.conf:/etc/nginx/conf.d/default.conf:ro nginx

# Verificar en http://localhost:8094 — solo "proxy" publica puerto hacia el host
```

**Punto clave:** el contenedor `app` (PHP-FPM) **no** publica ningún puerto con `-p`; solo es alcanzable dentro de la red `red-ej3-m5`, y únicamente `proxy` (Nginx) es accesible desde fuera, en el puerto 8094.
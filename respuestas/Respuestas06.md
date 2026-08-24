# Entornos, Rendimiento y Optimización
---
## Ejercicios prácticos

### Ejercicio 1: Monitoreo de recursos

```bash
docker run -d --name limitado --cpus="0.5" --memory="128m" nginx
docker run -d --name amplio --cpus="2" --memory="1g" nginx

# Generar carga de prueba (ejemplo con Apache Bench)
ab -n 5000 -c 100 http://localhost:8095/

docker stats limitado amplio --no-stream
```

**Observación esperada:** el contenedor `limitado` alcanzará su tope de CPU/memoria más rápido bajo carga (mayor tiempo de respuesta o posible reinicio por OOM si se excede la memoria), mientras que `amplio` sostiene la carga con métricas más holgadas en `docker stats`.

---

### Ejercicio 2: Auditoría de buenas prácticas

**Hallazgos típicos sobre el Dockerfile del Módulo 5:**

| Hallazgo | Corrección |
|---|---|
| El contenedor corre como `root` por defecto | Agregar `RUN useradd -m appuser` y `USER appuser` antes del `CMD`/`ENTRYPOINT` |
| No existe `.dockerignore` | Agregar uno con `.git`, `*.md`, archivos temporales |
| Imagen base no optimizada (`php:8.2-apache` es relativamente pesada) | Evaluar migrar a una variante `-alpine` si las extensiones lo permiten |

```dockerfile
FROM php:8.2-apache
WORKDIR /var/www/html
COPY src/ .
RUN useradd -m appuser && chown -R appuser:appuser /var/www/html
USER appuser
EXPOSE 80
```

---

### Ejercicio 3: Limpieza controlada del entorno

```bash
# Generar recursos "sucios" de prueba
docker run --name c1 alpine echo hola
docker run --name c2 alpine echo hola
docker pull alpine:3.18
docker volume create vol-huerfano

docker system df                 # estado antes de limpiar

docker container prune -f        # elimina c1 y c2 (detenidos)
docker image prune -f            # elimina imágenes "dangling"
docker volume prune -f           # elimina vol-huerfano (no referenciado)

docker system df                 # estado después de limpiar
```

**Diferenciación esperada:**
- `container prune` → solo contenedores **detenidos**.
- `image prune` → solo imágenes **sin tag** o no referenciadas (usar `-a` para todas las no usadas por ningún contenedor).
- `volume prune` → solo volúmenes **no montados** por ningún contenedor.

---
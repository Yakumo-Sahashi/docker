# Comandos: Entornos, Rendimiento y Optimización
---

## Monitoreo

| Comando | Descripción |
|---------|-------------|
| **`docker stats`** | Muestra en tiempo real el consumo de CPU, memoria, E/S de red y disco de los contenedores en ejecución. |
| **`docker logs`** | Permite revisar la salida histórica o en vivo (-f) de un contenedor para diagnosticar comportamiento. |
| **`docker inspect`** | Devuelve en formato JSON toda la configuración y el estado detallado de un contenedor, imagen, red o volumen. |
| **`docker stats --no-stream`** | Muestra las estadísticas de uso de los contenedores, pero solo toma una muestra y termina. |
| **`grep -A 5 '"Memory"'`** | Filtra la información relacionada con "Memory". |

---

## Buenas practicas
| Comando | Descripción |
|---------|-------------|
| **`docker container prune`** | Elimina contenedores detenidos |
| **`docker image prune`** | Elimina imágenes sin usar (dangling) |
| **`docker volume prune`** | Elimina volúmenes no referenciados |
| **`docker system prune -a`** | Limpieza general (usar con precaución) |

---

## Ejemplo

Comparar el comportamiento de un contenedor en modo desarrollo (con bind mount y sin límites) frente a uno en modo producción (imagen optimizada y con límites de recursos):

**Modo desarrollo:** bind mount, sin límites, logs visibles
```bash
docker run -d --name app-dev -p 8000:80 -v $(pwd)/src:/var/www/html mi-app:dev
docker logs -f app-dev
```

**Modo producción:** imagen optimizada, límites de recursos
```bash
docker run -d --name app-prod -p 8001:80 --cpus="1" --memory="256m" mi-app:prod
docker stats app-prod --no-stream
```
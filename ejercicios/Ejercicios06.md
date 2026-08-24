# Entornos, Rendimiento y Optimización
---
## Ejercicios prácticos

### Ejercicio 1: Monitoreo de recursos
Levanta dos contenedores de tu elección con distintos límites de CPU y memoria. Usa docker stats para comparar su consumo bajo carga (por ejemplo, generando tráfico con múltiples peticiones simultáneas con curl o ab). Documenta tus observaciones.

Criterios de logro:
- El estudiante identifica correctamente el efecto de los límites --cpus y --memory.
- Se documentan capturas o salidas de docker stats como evidencia.

---

### Ejercicio 2: Auditoría de buenas prácticas
Toma el Dockerfile construido en el Módulo 5 y audítalo contra la lista de buenas prácticas de este módulo (usuario no root, sin secretos embebidos, imagen base ligera, .dockerignore). Corrige al menos dos hallazgos y documenta el antes/después.

Criterios de logro:
- Se identifican correctamente al menos 2 mejoras aplicables.
- Las correcciones no rompen la funcionalidad de la imagen.

---

### Ejercicio 3: Limpieza controlada del entorno
Genera intencionalmente varios contenedores detenidos, imágenes sin usar y un volumen huérfano. Usa los comandos prune adecuados para limpiar cada tipo de recurso por separado, verificando con docker system df el espacio recuperado antes y después.

Criterios de logro:
- Se documenta el espacio en disco antes y después de la limpieza.
- El estudiante distingue qué recursos elimina cada comando prune.

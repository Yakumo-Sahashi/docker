# Dockerfile, Imágenes Personalizadas y Proxy Inverso
---
## Ejercicios prácticos

### Ejercicio 1: : Dockerfile básico para PHP
Crea un Dockerfile a partir de la imagen oficial php:8.2-apache que copie una aplicación PHP simple (puedes usar un 'Hola mundo' con phpinfo()) y construya la imagen con el tag practica-php:1.0. Verifica que el contenedor responde correctamente al levantarlo.

Criterios de logro:
- La imagen se construye sin errores.
- El contenedor responde correctamente en el navegador.

---

### Ejercicio 2: Optimización de capas
Toma el Dockerfile del ejercicio anterior y reordénalo aplicando el principio de capas cacheables (dependencias antes que código fuente). Agrega un archivo .dockerignore adecuado. Realiza dos builds consecutivos modificando solo el código fuente entre uno y otro, y documenta con capturas cómo el segundo build reutiliza capas cacheadas.

Criterios de logro:
- El Dockerfile sigue el orden recomendado de capas.
- El estudiante puede señalar en la salida del build qué pasos usaron caché.

---

### Ejercicio 3: Nginx como proxy inverso
Configura un contenedor Nginx como proxy inverso hacia tu contenedor PHP del ejercicio 1, usando una red Docker personalizada. Publica únicamente el puerto de Nginx (no publiques el puerto de PHP directamente) y verifica que las peticiones llegan correctamente al backend.

Criterios de logro:
- Solo el contenedor Nginx expone puertos hacia el host.
- El proxy reenvía correctamente las peticiones al backend PHP.


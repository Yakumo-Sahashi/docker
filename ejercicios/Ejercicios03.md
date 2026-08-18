# Imagenes, Volumenes y Redes
---
## Ejercicios prácticos

### Ejercicio 1: Persistencia con volúmenes
Levanta un contenedor MySQL con un volumen nombrado. Crea una base de datos y una tabla con algunos registros. Elimina el contenedor (sin eliminar el volumen) y vuelve a crear uno nuevo apuntando al mismo volumen. Verifica que los datos siguen presentes.

Criterios de logro:
- Los datos persisten correctamente tras eliminar y recrear el contenedor.
- El estudiante explica por qué ocurre esto en términos del ciclo de vida del volumen.

---

### Ejercicio 2: Bind mount para desarrollo
Crea un contenedor Nginx que sirva un archivo index.html mediante un bind mount hacia una carpeta local. Modifica el archivo desde tu editor local y verifica que el cambio se refleja de inmediato al recargar el navegador, sin reiniciar el contenedor.

Criterios de logro:
- El cambio se refleja sin necesidad de reconstruir o reiniciar el contenedor.
- El estudiante distingue correctamente cuándo usar bind mount vs. volumen Docker.

---

### Ejercicio 3: PHP + MySQL en red personalizada
Replica la demostración: crea una red personalizada, levanta un contenedor MySQL y uno PHP conectados a ella, y desde un script PHP simple confirma la conexión exitosa a la base de datos usando el nombre del contenedor MySQL como host.

Criterios de logro:
- La conexión PHP-MySQL se establece exitosamente usando el nombre del contenedor.
- El estudiante explica el rol del DNS interno de Docker en este escenario.

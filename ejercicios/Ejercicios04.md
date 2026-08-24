# Imagenes, Volumenes y Redes
---
## Ejercicios prácticos

### Ejercicio 1: Primer compose.yml

Escribe un archivo compose.yml que levante un servicio Nginx (imagen oficial) publicado en el puerto de tu elección y un servicio Redis, ambos en la misma red definida por el usuario. Levanta el entorno con docker compose up -d y confirma con docker compose ps que ambos servicios están corriendo.
Criterios de logro:
- El archivo YAML es válido y ambos servicios inician sin errores.
- El estudiante puede explicar cómo se comunicarían entre sí ambos servicios si fuera necesario.

---

### Ejercicio 2: Variables de entorno con *.env*
Modifica el ejercicio anterior para parametrizar el puerto publicado de Nginx y el nombre del proyecto mediante variables definidas en un archivo .env. Levanta el entorno y confirma que los valores se están tomando del archivo.
Criterios de logro:
- Las variables se resuelven correctamente desde el archivo .env.
- El estudiante entrega también un .env.example sin datos sensibles.

---

### Ejercicio 3: Réplica del stack PHP + MySQL
A partir de la demostración, construye tu propio compose.yml con los tres servicios (Nginx, PHP, MySQL), usando volúmenes para persistencia de la base de datos y variables de entorno para las credenciales. Añade datos a la bd y mediante un archivo index.php y realiza una conexion a la bd y muestra su contenido.
Documenta el proceso de levantamiento y verificación.
Criterios de logro:
- Los tres servicios se comunican correctamente entre sí.
- Los datos de MySQL persisten tras un docker compose down sin -v seguido de un docker compose up.

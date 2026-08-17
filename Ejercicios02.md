# Instalación y Gestión de Docker
---
## Ejercicios prácticos

### 1. Ciclo de vida completo
- Crea un contenedor Nginx con un nombre personalizado, publícalo en el puerto 9090, verifica su estado con docker **``ps``**, detenlo, vuelve a iniciarlo, revisa sus logs y finalmente elimínalo. Documenta cada comando utilizado y su salida.
- **Criterios de logro:**
•	Se ejecutan correctamente todas las transiciones de estado del contenedor.
•	El puerto 9090 responde mientras el contenedor está activo.

---

### 2. Exploración interna
- Levanta un contenedor de la imagen alpine en modo interactivo (docker run -it alpine sh), explora su sistema de archivos con comandos básicos de Linux (ls, cat /etc/os-release, ps) y sal del contenedor. Investiga qué ocurre con el contenedor una vez que sales.

- **Criterios de logro:**
•	El estudiante identifica que al salir de un contenedor interactivo sin proceso en segundo plano, este pasa a estado Exited.
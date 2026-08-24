# Registry y Distribución de Imágenes

---
## Ejercicios prácticos

### Ejercicio 1: Publicar una imagen propia

```bash
docker login

docker tag practica-php:1.0 miusuario/practica-php:1.0

docker push miusuario/practica-php:1.0
```

Entregable: enlace del tipo `https://hub.docker.com/r/miusuario/practica-php`.

---

### Ejercicio 2: Distribución cruzada

**Estudiante A** publica su imagen; 
**Estudiante B** la descarga y ejecuta:

```bash
docker pull miusuarioA/practica-php:1.0
docker run -d -p 8096:80 miusuarioA/practica-php:1.0
# Verificar en http://localhost:8096 sin haber tocado el Dockerfile original
```

**Evidencia esperada:** captura de pantalla mostrando la aplicación funcionando en el equipo B, junto con `docker images` confirmando que la imagen proviene del repositorio del compañero.

---

### Ejercicio 3: Distribución sin registry

```bash
docker save -o practica-php.tar practica-php:1.0
# transferir practica-php.tar por USB/red local
docker load -i practica-php.tar
docker run -d -p 8097:80 practica-php:1.0
```

| Método | Ventajas | Desventajas |
|---|---|---|
| Registry (`push`/`pull`) | Centralizado, versionado, accesible desde cualquier lugar con red, ideal para CI/CD | Requiere cuenta/autenticación y conectividad a Internet (o a un registry interno) |
| `save`/`load` (archivo .tar) | No depende de conectividad ni de un servicio externo, útil en redes aisladas | Manual, no versionado automáticamente, requiere transferir el archivo físicamente o por otro canal |

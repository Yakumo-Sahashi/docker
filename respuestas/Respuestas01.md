# Introducción a Docker
---
## Ejercicios prácticos

### 1. Primer contacto con Docker
```bash
docker run hello-world
```
Explicación esperada del estudiante:

1. El Docker CLI envía la instrucción run hello-world al Docker Daemon a través de la API REST.
2. El daemon busca la imagen hello-world localmente; al no encontrarla, la descarga (pull) desde Docker Hub.
3. El daemon crea un contenedor nuevo a partir de esa imagen.
4. El contenedor ejecuta su proceso por defecto (imprime el mensaje de bienvenida en stdout).
5. El proceso termina inmediatamente después de imprimir el mensaje, por lo que el contenedor pasa a estado Exited (0).
6. La salida que ve el usuario viaja de vuelta: contenedor → daemon → CLI → terminal.

---
### 2. Nginx en segundo plano
Levantar el contenedor publicando el puerto 8081
```bash
docker run -d --name nginx-ej2 -p 8081:80 nginx
```
Verificar que responde
```bash
curl http://localhost:8081
```
o abrir http://localhost:8081 en el navegador

Revisar logs
```bash
docker logs nginx-ej2
```

Detener y eliminar
```bash
docker stop nginx-ej2
docker rm nginx-ej2
```

**Nota:** *docker stop envía SIGTERM (y tras un tiempo de gracia, SIGKILL) deteniendo el contenedor pero conservándolo en estado Exited; docker rm lo elimina definitivamente del sistema, incluyendo su capa de escritura.*

---

### 3. Cuadro comparativo
| Criterio | Contenedores (Docker) | Máquinas Virtuales |
|---|---|---|
| Kernel | Comparten el kernel del host | Cada VM tiene su propio kernel |
| Peso típico | Decenas/cientos de MB | Varios GB |
| Tiempo de arranque | Segundos | Minutos |
| Aislamiento | A nivel de proceso (namespaces/cgroups) | A nivel de hardware virtualizado (más fuerte) |
| Densidad por host | Alta (decenas/cientos) | Baja/media (pocas por host físico) |

**Ejemplos de uso sugeridos:**
- **Contenedores:** microservicios de una aplicación web que necesitan desplegarse y escalar rápidamente (ej. una API de e-commerce en horas pico).
- **VMs:** ejecutar sistemas operativos distintos entre sí en el mismo host físico, o cuando se requiere aislamiento fuerte a nivel de kernel (ej. multi-tenancy en un proveedor de hosting).

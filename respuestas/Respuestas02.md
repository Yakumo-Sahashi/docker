# Instalación y Gestión de Docker
---
## Ejercicios prácticos

### 1. Ciclo de vida completo

Crear el contenedor publicado en el puerto 9090
```bash
docker run -d --name mi-web -p 9090:80 nginx
```
Verificar estado
```bash
docker ps
```

Detener
```bash
docker stop mi-web
docker ps -a          # confirmar que aparece como "Exited"
```

Volver a iniciar
```bash
docker start mi-web
docker ps              # confirmar que vuelve a "Up"
```
Revisar logs
```bash
docker logs mi-web
```

Eliminar
```bash
docker stop mi-web
docker rm mi-web
```

---

### 2. Exploración interna
```bash
docker run -it alpine sh
```
Dentro del contenedor:
```bash
ls /
cat /etc/os-release
ps
exit
```

```bash
docker ps -a
```

**Respuesta esperada:** *al ejecutar exit, el proceso principal del contenedor (el propio sh) termina, y como no hay ningún otro proceso en segundo plano, el contenedor completo pasa a estado Exited. Esto ilustra que un contenedor vive mientras viva su proceso principal (PID 1).*
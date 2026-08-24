# Comandos: Dockerfile, Imágenes Personalizadas y Proxy Inverso
---

## Instrucciones Dockerfile

| Comando | Descripción |
|---------|-------------|
| **`FROM`** | Define la imagen base sobre la que se construye la nueva imagen. Siempre es la primera instrucción significativa. |
| **`RUN`** | Ejecuta un comando durante la construcción de la imagen (por ejemplo, instalar paquetes) y persiste su resultado como una nueva capa. |
| **`COPY`** | Copia archivos o carpetas desde el contexto de build hacia el sistema de archivos de la imagen. |
| **`ADD`** | Similar a COPY, pero además soporta descomprimir archivos .tar automáticamente y descargar URLs remotas. Se recomienda usar COPY salvo que se necesite explícitamente esa funcionalidad extra. |
| **`WORKDIR`** | Define el directorio de trabajo dentro del contenedor para las instrucciones siguientes (y para docker exec). |
| **`ENV`** | Define variables de entorno persistentes, disponibles tanto durante el build como en tiempo de ejecución del contenedor. |
| **`EXPOSE`** | Documenta el puerto en el que la aplicación escuchará dentro del contenedor (no publica el puerto por sí solo, es informativo). |
| **`CMD`** | Define el comando por defecto que se ejecuta al iniciar el contenedor; puede sobreescribirse al ejecutar docker run. |
| **`ENTRYPOINT`** | Define el proceso principal e inmutable del contenedor; CMD puede usarse en conjunto para pasarle argumentos por defecto. |

## Construcción de la imagen

```bash
docker build -t mi-app:1.0 .
docker build -t mi-app:1.0 -f Dockerfile.prod .
```

El punto (.) al final indica el 'contexto de build': la carpeta cuyo contenido se envía al daemon y desde la cual COPY/ADD pueden tomar archivos.

---

## Ejemplo

Construir una imagen personalizada de PHP y usarla detrás de un proxy inverso Nginx:
1. Construir la imagen personalizada
```bash
docker build -t mi-php:1.0 ./app
```

2. Verificar la imagen creada
```bash
docker images | grep mi-php
```

3. Levantar app (mi-php) + proxy Nginx en una red compartida
```bash
docker network create red-demo
docker run -d --name app --network red-demo mi-php:1.0
docker run -d --name proxy --network red-demo -p 8080:80 \
  -v $(pwd)/nginx.conf:/etc/nginx/conf.d/default.conf:ro nginx:latest
```

4. Probar en el navegador: http://localhost:8080
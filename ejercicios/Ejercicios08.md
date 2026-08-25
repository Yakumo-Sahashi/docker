# Proyecto Integrador
---

## Arquitectura del proyecto
El proyecto integrador reproduce un escenario profesional típico: una aplicación Laravel servida por PHP-FPM, expuesta a través de Nginx como proxy inverso, con persistencia de datos en MySQL. Toda la arquitectura se define y orquesta mediante Docker Compose.

```
Cliente (navegador)
      │
      ▼
  [ Nginx ]  ← proxy inverso, puerto publicado 8080:80
      │  fastcgi_pass
      ▼
  [ PHP-FPM / Laravel ]  ← imagen personalizada (Dockerfile propio)
      │
      ▼
  [ MySQL ]  ← con volumen persistente

```

---

## Requisitos técnicos del proyecto

- Un Dockerfile propio para el servicio de aplicación (PHP/Laravel), siguiendo buenas prácticas de capas y, si aplica, multi-stage build.
- Un archivo docker-compose.yml que orqueste los tres servicios (nginx, app, db).
- Configuración personalizada de Nginx como proxy inverso hacia PHP-FPM.
- Configuración de PHP/Laravel apuntando a la base de datos mediante variables de entorno.
- Configuración de MySQL con usuario, base de datos y contraseña parametrizados.
- Una red Docker definida por el usuario que conecte los tres servicios.
- Un volumen nombrado para persistir los datos de MySQL.
- Variables de entorno gestionadas mediante un archivo .env (no versionado con datos reales).
- Una imagen personalizada final, publicada en un registry (Docker Hub o privado).

---

## Actividades guiadas

1.	Analizar la aplicación Laravel proporcionada (o una base mínima de Laravel generada con composer create-project): identificar requisitos de PHP, extensiones necesarias y variables de configuración (.env de Laravel).
2.	Crear el Dockerfile del servicio de aplicación, partiendo de una imagen oficial de PHP-FPM, instalando extensiones necesarias (pdo_mysql, mbstring, etc.) y Composer.
3.	Crear el archivo docker-compose.yml con los tres servicios, sus dependencias, redes y volúmenes.
4.	Configurar PHP para exponer el puerto 9000 (PHP-FPM) y montar el código de la aplicación.
5.	Configurar Nginx como proxy inverso hacia el servicio 'app' en el puerto 9000, publicando el puerto 80 del contenedor hacia el 8080 del host.
6.	Configurar el servicio MySQL con las variables de entorno correspondientes (usuario, base de datos, contraseña) tomadas del archivo .env.
7.	Crear la red Docker personalizada que conecte los tres servicios entre sí.
8.	Crear el volumen nombrado para persistir /var/lib/mysql.
9.	Levantar todos los servicios con docker compose up -d y verificar el estado con docker compose ps.
10.	Probar la aplicación desde el navegador (http://localhost:8080), validando que las páginas cargan y que Laravel logra conectarse a la base de datos.
11.	Generar la imagen final del servicio de aplicación con un tag versionado (por ejemplo, mi-laravel-app:1.0).
12.	Distribuir la imagen: publicarla en Docker Hub (o un registro privado) y descargarla/ejecutarla desde otro equipo o entorno para confirmar su portabilidad.


---

## Estructura de archivos sugerida

```
proyecto-integrador/
├── docker-compose.yml
├── .env
├── .env.example
├── nginx/
│   └── default.conf
└── app/
    ├── Dockerfile
    ├── .dockerignore
    └── (código fuente de Laravel)

```

---

## Rúbrica de evaluación

| Criterio | Descripcion |
|----------|-------------|
| **Arquitectura (25%)** | Los tres servicios están correctamente definidos, conectados por una red propia y con dependencias declaradas. |
| **Dockerfile (20%)** | Sigue buenas prácticas: orden de capas, .dockerignore, imagen base adecuada, sin secretos embebidos. |
| **Persistencia y configuración (20%)** | Volumen de MySQL funcional; variables de entorno correctamente parametrizadas vía .env. |
| **Funcionalidad (20%)** | La aplicación carga correctamente y logra conectarse a la base de datos a través del proxy inverso. |
| **Distribución (15%)** | La imagen final se publica y se descarga/ejecuta exitosamente desde un entorno distinto al original. |

---

## Entregables

- Repositorio (o carpeta comprimida) con todo el código fuente, Dockerfile, compose.yml y configuración de Nginx (sin incluir el .env real).
- Archivo .env.example documentando todas las variables necesarias.
- Breve documento (README) explicando cómo levantar el proyecto desde cero: docker compose up -d y pasos adicionales si los hubiera.
- Enlace a la imagen publicada en el registry utilizado.
- Capturas de pantalla o evidencia de la aplicación funcionando en el navegador.

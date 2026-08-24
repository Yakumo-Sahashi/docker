# Comandos: Registry y Distribución de Imágenes

---

## Monitoreo

| Comando | Descripción |
|---------|-------------|
| **`docker login`** | Autentica al usuario contra un registry (Docker Hub por defecto, u otro indicando su URL). |
| **`docker tag`** | Crea una referencia adicional (tag) a una imagen local, típicamente con el formato usuario/repositorio:tag necesario para publicarla. |
| **`docker push`** | Sube una imagen etiquetada hacia el registry correspondiente. |
| **`docker pull`** | Descarga una imagen (o una versión específica) desde un registry. |
| **`docker save`** | Exporta una imagen a un archivo .tar, útil para transferirla sin pasar por un registry. |
| **`docker load`** | Importa una imagen previamente exportada con docker save. |

---

## Ejemplo

1. Iniciar sesión en Docker Hub
```bash
docker login
```

2. Etiquetar la imagen construida en el Módulo 5
```bash
docker tag mi-php:1.0 miusuario/mi-php:1.0
```

3. Publicarla en el registry
```bash
docker push miusuario/mi-php:1.0
```

4. Desde otro equipo (o simulando uno, eliminando la imagen local)
```bash
docker rmi miusuario/mi-php:1.0
docker pull miusuario/mi-php:1.0
docker run -d -p 8080:80 miusuario/mi-php:1.0
```

---

Alternativa sin registry: exportar/importar directamente
```bash
docker save -o mi-php-1.0.tar miusuario/mi-php:1.0
docker load -i mi-php-1.0.tar
```
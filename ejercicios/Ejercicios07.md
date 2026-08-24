# Registry y Distribución de Imágenes
---
## Ejercicios prácticos

### Ejercicio 1: Publicar una imagen propia

Crea una cuenta gratuita en Docker Hub (si no cuentas con una), etiqueta la imagen construida en el Módulo 5 con tu usuario, autentícate y publícala. Comparte el enlace público de tu repositorio.

Criterios de logro:
- La imagen es visible públicamente en Docker Hub bajo el repositorio del estudiante.
- El tag corresponde correctamente a la versión construida.

---

### Ejercicio 2: Distribución cruzada
En parejas, cada estudiante descarga (docker pull) la imagen publicada por su compañero y la ejecuta localmente sin ninguna modificación, verificando que se comporta exactamente igual que en el equipo original.

Criterios de logro:
- La imagen descargada funciona sin necesidad de ajustes adicionales.
- Se documenta evidencia de la ejecución exitosa en un equipo distinto al de origen.

---

### Ejercicio 3: Distribución sin registry
Exporta tu imagen a un archivo .tar con docker save, transfiérela por otro medio (USB, red local) a otro equipo y cárgala ahí con docker load. Compara este flujo con el uso de un registry y documenta ventajas/desventajas de cada enfoque.

Criterios de logro:
- El archivo .tar se genera, transfiere y carga correctamente.
- Se identifican al menos 2 ventajas y 2 desventajas de cada método.

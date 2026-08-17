# Comandos Linux
---

## Navegación y Gestión de Archivos

| Comando | Descripción | Ejemplo |
|---------|-------------|---------|
| `pwd` | Muestra la ruta del directorio actual (print working directory) | `pwd` |
| `ls` | Lista los archivos y carpetas de un directorio | `ls -la /home/usuario` |
| `cd` | Cambia de directorio | `cd /var/log` |
| `mkdir` | Crea un nuevo directorio | `mkdir proyectos` |
| `rmdir` | Elimina un directorio vacío | `rmdir proyectos_viejos` |
| `rm` | Elimina archivos o directorios | `rm -rf carpeta_temp` |
| `cp` | Copia archivos o directorios | `cp archivo.txt respaldo.txt` |
| `mv` | Mueve o renombra archivos/directorios | `mv archivo.txt /home/usuario/documentos/` |
| `touch` | Crea un archivo vacío o actualiza su fecha de modificación | `touch nuevo_archivo.txt` |
| `find` | Busca archivos y directorios según criterios | `find / -name "*.log"` |
| `locate` | Busca archivos rápidamente usando una base de datos indexada | `locate archivo.conf` |

--- 

## Visualización y Edición de Archivos

| Comando | Descripción | Ejemplo |
|---------|-------------|---------|
| `cat` | Muestra el contenido completo de un archivo | `cat /etc/hostname` |
| `less` | Muestra el contenido de un archivo página por página | `less archivo_grande.txt` |
| `head` | Muestra las primeras líneas de un archivo | `head -n 10 archivo.log` |
| `tail` | Muestra las últimas líneas de un archivo | `tail -f /var/log/syslog` |
| `nano` | Editor de texto simple en terminal | `nano config.txt` |
| `vim` | Editor de texto avanzado en terminal | `vim script.sh` |
| `grep` | Busca patrones de texto dentro de archivos | `grep "error" archivo.log` |
| `wc` | Cuenta líneas, palabras y caracteres de un archivo | `wc -l archivo.txt` |
| `diff` | Compara el contenido de dos archivos | `diff archivo1.txt archivo2.txt` |

---

## Permisos y Propiedad

| Comando | Descripción | Ejemplo |
|---------|-------------|---------|
| `chmod` | Cambia los permisos de un archivo o directorio | `chmod 755 script.sh` |
| `chown` | Cambia el propietario de un archivo o directorio | `chown usuario:grupo archivo.txt` |
| `chgrp` | Cambia el grupo propietario de un archivo | `chgrp desarrolladores proyecto/` |
| `umask` | Define los permisos por defecto para nuevos archivos | `umask 022` |

---

## Procesos y Sistema

| Comando | Descripción | Ejemplo |
|---------|-------------|---------|
| `ps` | Muestra los procesos en ejecución | `ps aux` |
| `top` | Muestra procesos en tiempo real con uso de recursos | `top` |
| `htop` | Versión interactiva y mejorada de top | `htop` |
| `kill` | Termina un proceso mediante su PID | `kill -9 1234` |
| `killall` | Termina procesos por nombre | `killall firefox` |
| `df` | Muestra el espacio en disco disponible | `df -h` |
| `du` | Muestra el uso de espacio de archivos/directorios | `du -sh /home/usuario` |
| `free` | Muestra el uso de memoria RAM y swap | `free -h` |
| `uptime` | Muestra el tiempo de actividad del sistema | `uptime` |
| `uname` | Muestra información del sistema operativo | `uname -a` |

---

## Redes

| Comando | Descripción | Ejemplo |
|---------|-------------|---------|
| `ping` | Verifica la conectividad con otro host | `ping google.com` |
| `ifconfig` / `ip` | Muestra o configura interfaces de red | `ip addr show` |
| `curl` | Transfiere datos desde o hacia un servidor | `curl -O https://ejemplo.com/archivo.zip` |
| `wget` | Descarga archivos desde la web | `wget https://ejemplo.com/archivo.zip` |
| `ssh` | Conecta a otro equipo de forma remota y segura | `ssh usuario@192.168.1.10` |
| `scp` | Copia archivos entre equipos vía SSH | `scp archivo.txt usuario@servidor:/ruta/` |
| `netstat` | Muestra conexiones de red activas | `netstat -tulnp` |

---

## Compresión y Archivos

| Comando | Descripción | Ejemplo |
|---------|-------------|---------|
| `tar` | Empaqueta y/o comprime archivos y directorios | `tar -czvf backup.tar.gz /home/usuario/proyecto` |
| `zip` | Comprime archivos en formato .zip | `zip -r archivo.zip carpeta/` |
| `unzip` | Descomprime archivos .zip | `unzip archivo.zip` |
| `gzip` | Comprime archivos individuales | `gzip archivo.txt` |

---

## Usuarios y Permisos de Sistema

| Comando | Descripción | Ejemplo |
|---------|-------------|---------|
| `sudo` | Ejecuta un comando con privilegios de administrador | `sudo apt update` |
| `su` | Cambia al usuario especificado (o root) | `su usuario2` |
| `useradd` | Crea un nuevo usuario | `sudo useradd -m nuevo_usuario` |
| `passwd` | Cambia la contraseña de un usuario | `passwd usuario` |
| `whoami` | Muestra el usuario actual | `whoami` |
| `who` | Muestra los usuarios conectados al sistema | `who` |

---

## Gestión de Paquetes (Debian/Ubuntu)

| Comando | Descripción | Ejemplo |
|---------|-------------|---------|
| `apt update` | Actualiza la lista de paquetes disponibles | `sudo apt update` |
| `apt upgrade` | Actualiza los paquetes instalados | `sudo apt upgrade` |
| `apt install` | Instala un nuevo paquete | `sudo apt install nginx` |
| `apt remove` | Desinstala un paquete | `sudo apt remove nginx` |

---

## Otros Comandos Útiles

| Comando | Descripción | Ejemplo |
|---------|-------------|---------|
| `history` | Muestra el historial de comandos ejecutados | `history` |
| `alias` | Crea un alias para un comando | `alias ll='ls -la'` |
| `man` | Muestra el manual de un comando | `man ls` |
| `echo` | Imprime texto o el valor de una variable | `echo "Hola mundo"` |
| `clear` | Limpia la pantalla de la terminal | `clear` |
| `date` | Muestra o configura la fecha y hora del sistema | `date` |
| `crontab` | Programa tareas automáticas | `crontab -e` |

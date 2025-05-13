
🧩 Arquitectura del sistema

+=====================================================================================+
|                                      VIRTUALBOX                                     |
|=====================================================================================|
|                                                                                     |
|  +-------------------------+           FTP           +---------------------------+  |
|  |   Ubuntu Server 22.04   |  -------------------->  |         TrueNAS           |  |
|  |-------------------------|                         |---------------------------|  |
|  | - MySQL Esclavo         |                         | - Carpeta: /Backups       |  |
|  | - Script de backup.sh   |                         | - Discos en espejo (RAID) |  |
|  | - Cronjob               |                         +---------------------------+  |
|  |                         |                                                        |
|  |   +------------------+  |                                                        | 
|  |   |   Docker         |  |                                                        |
|  |   |   Container      |  |                                                        |
|  |   |   mysql-master   |  |                                                        |
|  |   +------------------+  |                                                        |
|  +-------------------------+                                                        |
|                                                                                     |
+=====================================================================================+


🛠️ Puesta en marcha del sistema

# 🔌 Iniciar MySQL (esclavo en Ubuntu host)

- sudo systemctl start mysql

# 🔌 Iniciar el servicio de cron (para ejecutar backups automáticamente)

- sudo systemctl start cron

# 🐳 Iniciar el contenedor MySQL maestro
Iniciar el contenedor Docker (MySQL Maestro)

- sudo docker start mysql-master

# ⚙️ Acceder al contenedor MySQL maestro

- sudo docker exec -it mysql-master mysql -u root -p

⚙️ Tecnologías utilizadas

    Ubuntu Server 22.04 – Sistema base y entorno de ejecución.

    MySQL 8.x (Maestro en Docker, Esclavo en Host) – Sistema de gestión de bases de datos.

    Docker – Para contenerizar el servidor MySQL maestro (mysql-master).

    TrueNAS – NAS con discos en espejo para almacenamiento seguro de backups.

    FTP – Protocolo usado para transferir backups desde Ubuntu hacia TrueNAS.

    cron – Utilizado para ejecutar tareas automáticas programadas (backups).

📁 Estructura general

    backup.sh – Script que realiza el dump de la base de datos MySQL esclavo y lo envía vía FTP a la NAS.

    cron – Configuración de la tarea cron que ejecuta el script automáticamente.

    /Backups – Carpeta en la NAS donde se almacenan los archivos .sql generados.
🔒 Credenciales de ejemplo

    Ubuntu Server 22.04

Usuario: whu
Contraseña: password

NAS (TrueNAS)

Usuario: truenas_admin
Contraseña: password
Ruta FTP: /Backups

FTP desde Ubuntu hacia NAS

Usuario: whu
Contraseña: passwordwhu

MySQL

    Maestro (Docker container mysql-master)

Usuario: root
Contraseña: password

Esclavo (Instalado en Ubuntu host)

Usuario: root
Contraseña: password


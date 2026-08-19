🧩 System Architecture

```text
+=====================================================================================+
|                                      VIRTUALBOX                                     |
|=====================================================================================|
|                                                                                     |
|  +-------------------------+           FTP           +---------------------------+  |
|  |   Ubuntu Server 22.04   |  -------------------->  |         TrueNAS           |  |
|  |-------------------------|                         |---------------------------|  |
|  | - MySQL Slave           |                         | - Folder: /Backups       |  |
|  | - backup.sh Script      |                         | - Mirrored Disks (RAID)  |  |
|  | - Cronjob               |                         +---------------------------+  |
|  |                         |                                                        | 
|  |   +------------------+  |                                                        |
|  |   |      Docker      |  |                                                        |
|  |   |    Container     |  |                                                        |
|  |   |   mysql-master   |  |                                                        |
|  |   +------------------+  |                                                        |
|  +-------------------------+                                                        |
|                                                                                     |
+=====================================================================================+
```

🛠️ System Startup

# 🔌 Start MySQL (Slave on Ubuntu Host)

* sudo systemctl start mysql

# 🔌 Start the Cron Service (to execute backups automatically)

* sudo systemctl start cron

# 🐳 Start the MySQL Master Container

Start the Docker container running the MySQL Master:

* sudo docker start mysql-master

# ⚙️ Access the MySQL Master Container

* sudo docker exec -it mysql-master mysql -u root -p

⚙️ Technologies Used

```
Ubuntu Server 22.04 – Base operating system and execution environment.

MySQL 8.x (Master in Docker, Slave on Host) – Database management system.

Docker – Used to containerize the MySQL Master server (mysql-master).

TrueNAS – NAS with mirrored disks for secure backup storage.

FTP – Protocol used to transfer backups from Ubuntu to TrueNAS.

cron – Used to execute scheduled tasks automatically (backups).
```

📁 General Structure

```
backup.sh – Script that creates a dump of the MySQL Slave database and sends it via FTP to the NAS.

cron – Cron configuration used to execute the backup script automatically.

/Backups – Folder on the NAS where the generated .sql files are stored.
```

# 🔒 Credentials

```
Ubuntu Server 22.04
```

Username: whu
Password: password

NAS (TrueNAS)

Username: truenas_admin
Password: password
FTP Path: /Backups

FTP from Ubuntu to NAS

Username: whu
Password: passwordwhu

MySQL

```
Master (Docker container mysql-master)
```

Username: root
Password: password

Slave (Installed on Ubuntu Host)

Username: root
Password: password

# OVA Download Link

https://mega.nz/file/WMUR0JrZ#-MnLdN1pVIv0mgGKW4jQUFRSX1txKsEy_RVWY1YMp4w

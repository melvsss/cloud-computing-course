# Mission 10: Enterprise Cloud Architecture

## Project Overview

This project is part of the CCM101 – Cloud Computing course. It demonstrates the deployment of a multi-tier cloud infrastructure using Ubuntu Server, Docker, WordPress, and MariaDB.

The main goal is to build a secure, automated, observable, and persistent cloud environment using virtualization and containerization.

## System Architecture

The infrastructure follows this architecture:

1. **Host Computer:** Windows computer used to access the application through a web browser.
2. **Virtualization:** VirtualBox runs the Ubuntu Server virtual machine.
3. **Operating System:** Ubuntu Server hosts Docker Engine and UFW Firewall.
4. **Application Layer:** WordPress runs inside a Docker container.
5. **Database Layer:** MariaDB stores application data in a separate Docker container.
6. **Persistent Storage:** Docker volumes preserve WordPress and database data.

## Technologies Used

- Oracle VirtualBox
- Ubuntu Server
- Docker Engine
- Docker Compose
- WordPress
- MariaDB
- UFW Firewall
- Bash Shell Scripting
- Cron
- GitHub

## Project Structure

```text
Mission 10 - Enterprise Cloud Architecture/
│
├── README.md
├── documentation/
├── diagrams/
├── docker/
└── screenshots/
```

## Security Implementation

- UFW Firewall is used to control incoming network connections.
- SSH access is used for remote server administration.
- Docker containers separate the application and database services.
- Database credentials are stored in an environment file.
- Sensitive configuration files are excluded from GitHub.

## Persistent Storage

Docker volumes are used to preserve application and database information even when containers are restarted or recreated.

- `wordpress_data`
- `mysql_data` (or the actual database volume name configured in Docker Compose)

## Backup and Recovery

A Bash backup script is used to export the MariaDB database and compress the SQL dump into a `.sql.gz` archive.

The project also uses Cron to schedule automated backups.

## Deployment Environment

- Hypervisor: VirtualBox
- Server: Ubuntu Server
- Container Platform: Docker Compose
- Application: WordPress
- Database: MariaDB

## Project Author

CCM101 – Cloud Computing  
Mission 10: Enterprise Cloud Architecture

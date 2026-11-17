# CCM101 – Mission 10: Enterprise Cloud Architecture

**Course:** CCM101 – Cloud Computing  
**Project:** Secure, Automated, and Observable Multi-Tier Cloud Infrastructure  
**Application Stack:** WordPress + MariaDB  
**Virtualization Platform:** Oracle VirtualBox  
**Operating System:** Ubuntu Server

---

## 1. Project Overview

This project demonstrates the deployment of a multi-tier cloud infrastructure using virtualization and containerization technologies.

The infrastructure runs on an Ubuntu Server virtual machine hosted through Oracle VirtualBox. Docker Compose manages the application and database containers, while UFW provides firewall protection.

The project also includes persistent storage, database backup scripting, and automated backup scheduling.

## 2. Project Objectives

- Deploy a Linux-based server using virtualization.
- Configure Docker Engine and Docker Compose.
- Deploy WordPress and MariaDB as separate containers.
- Configure persistent storage for application and database data.
- Implement firewall rules using UFW.
- Create a Bash script for database backups.
- Schedule automated backups using Cron.
- Document the infrastructure and its verification procedures.

## 3. System Architecture

The infrastructure follows a multi-tier architecture:

1. **Host Machine:** Windows 11 computer.
2. **Hypervisor:** Oracle VirtualBox.
3. **Virtual Machine:** Ubuntu Server.
4. **Security Layer:** UFW Firewall.
5. **Container Platform:** Docker Engine and Docker Compose.
6. **Application Layer:** WordPress.
7. **Database Layer:** MariaDB.
8. **Storage Layer:** Docker persistent volumes.

### Architecture Diagram

![Enterprise Cloud Architecture](diagrams/cloud-architecture.png)

## 4. Technologies Used

| Technology | Purpose |
|---|---|
| Windows 11 | Host operating system |
| VirtualBox | Virtualization |
| Ubuntu Server | Cloud server environment |
| Docker Engine | Container runtime |
| Docker Compose | Container orchestration |
| WordPress | Web application |
| MariaDB | Database management |
| UFW | Firewall management |
| Bash | Backup automation |
| Cron | Scheduled tasks |
| GitHub | Project documentation |

## 5. Infrastructure Configuration

### Virtual Machine

- Hypervisor: Oracle VirtualBox
- Guest Operating System: Ubuntu Server
- Network Mode: NAT
- SSH Access: Configured through VirtualBox port forwarding

### Accessing the Server

From Windows PowerShell:

```bash
ssh -p 2222 group5@127.0.0.1
```

### Accessing the Web Application

Open the configured forwarded web address in a browser:

```text
http://127.0.0.1:8080
```

*Confirm the actual VirtualBox port forwarding settings before using these values in your final demonstration.*

## 6. Docker Deployment

Docker Compose is used to manage the WordPress and MariaDB services.

### Project Directory

```bash
cd /opt/ccm101-cloud
```

### Verify Docker

```bash
sudo docker --version
sudo docker compose version
```

### Validate Docker Compose Configuration

```bash
sudo docker compose config -q
```

### Start the Containers

```bash
sudo docker compose up -d
```

### Check Container Status

```bash
sudo docker compose ps
```

### View Container Logs

```bash
sudo docker compose logs
```

## 7. Application and Database Architecture

### WordPress

WordPress provides the web application interface and runs in its own Docker container.

### MariaDB

MariaDB provides database services for WordPress and runs in a separate container.

The application communicates with the database through the internal Docker network.

Database credentials are stored in the server's environment configuration and must not be published in this repository.

## 8. Persistent Storage

Docker volumes provide persistent storage for application and database information.

The configured database volume is:

```text
ccm101-cloud_db_data
```

The actual WordPress volume name and mount configuration should be confirmed from the Docker Compose file.

### Verify Volumes

```bash
sudo docker volume ls
```

### Inspect a Volume

```bash
sudo docker volume inspect ccm101-cloud_db_data
```

Persistent volumes help preserve data when containers are restarted or recreated.

## 9. Security Implementation

### UFW Firewall

UFW is used to manage incoming and outgoing network traffic.

### Check Firewall Status

```bash
sudo ufw status verbose
```

### Configured Firewall Rules

The intended configuration allows SSH and web access while denying unsolicited incoming connections.

```bash
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw status
```

Only the ports required by the deployment should be exposed.

### Security Practices

- Keep database credentials outside the GitHub repository.
- Do not upload `.env` files.
- Restrict unnecessary network access.
- Use separate containers for application and database services.
- Use firewall rules to control incoming traffic.
- Keep Docker images and Ubuntu packages updated.

## 10. Database Backup and Recovery

A Bash script is used to export the MariaDB database and compress the SQL dump into a backup archive.

### Backup Directory

```text
/opt/ccm101-cloud/backups/
```

### Backup File Format

```text
wordpress-YYYY-MM-DD_HH-MM-SS.sql.gz
```

### Verify Backup Files

```bash
ls -lh /opt/ccm101-cloud/backups/
```

### Verify Compressed Backup Integrity

```bash
gzip -t /opt/ccm101-cloud/backups/wordpress-manual-backup.sql.gz
```

A successful integrity check indicates that the compressed archive is readable. A separate restore test is still required to verify database recovery.

## 11. Automated Backup Scheduling

Cron can execute the backup script automatically at a scheduled time.

### Open the Root Crontab

```bash
sudo crontab -e
```

### Daily Backup Schedule

```cron
0 2 * * * /opt/ccm101-cloud/backup.sh >> /var/log/ccm101-backup.log 2>&1
```

This schedule runs the backup script every day at 2:00 AM, according to the server's configured timezone.

### Verify Cron Configuration

```bash
sudo crontab -l
```

## 12. Monitoring and Verification

The following commands are used to inspect the infrastructure.

### Container Status

```bash
sudo docker compose ps
```

### Container Resource Usage

```bash
sudo docker stats --no-stream
```

### Database Health

```bash
sudo docker compose logs db
```

### Firewall Status

```bash
sudo ufw status verbose
```

### Storage Volumes

```bash
sudo docker volume ls
```

## 13. Screenshots and Evidence

Add screenshots of the actual deployment and verification results in this section.

Suggested evidence:

1. Ubuntu Server terminal.
2. Docker Compose container status.
3. MariaDB health status.
4. WordPress browser interface.
5. UFW firewall configuration.
6. Docker persistent volumes.
7. Successful database backup.
8. Cron scheduled backup configuration.
9. Backup integrity verification.

Example:

```markdown
![Docker Containers](screenshots/docker-containers.png)
```

## 14. Challenges and Solutions

| Challenge | Solution |
|---|---|
| Docker was initially unavailable inside Ubuntu Server | Installed Docker Engine inside the Ubuntu VM |
| VirtualBox clipboard sharing was unavailable | Used SSH from Windows PowerShell |
| Database backup was not completing as expected | Tested database export and compression separately |
| Port 80 was already in use | Investigated Docker port bindings and restarted the Docker service |

## 15. Conclusion

This project demonstrates the design and deployment of a multi-tier cloud infrastructure using VirtualBox, Ubuntu Server, Docker Compose, WordPress, and MariaDB.

It incorporates container isolation, firewall protection, persistent storage, database backup scripting, and scheduled automation.

The project provides practical experience in cloud infrastructure deployment, Linux administration, container management, and basic security operations.

---

**CCM101 – Cloud Computing**  
**Mission 10: Enterprise Cloud Architecture**

---
name: servers
description: |
  Server management e SSH workflow. Usare per SSH, gestione srv1/mnt1/nas,
  operazioni sistema, log analysis. Include srv1 (Ubuntu), mnt1 (Ubuntu), nas (TrueNAS Scale).
---

## Servers

| Server | OS | SSH Alias | Role | Access |
|--------|-----|-----------|------|--------|
| srv1 | Ubuntu | `ssh srv1` | Production server | Full (confirm per dangerous ops) |
| mnt1 | Ubuntu | `ssh mnt1` | Mount server | Full (confirm per dangerous ops) |
| nas | TrueNAS Scale | `ssh nas` | Home NAS | Read-only only |

## SSH Connection

```bash
ssh <server>  # srv1, mnt1, o nas
```

## Server-Specific Rules

### nas (TrueNAS Scale) - READ ONLY

**ALLOWED:**
- `zpool status`, `zfs list`, `df -h`
- `midclt call alert.query`
- `smbstatus`, `showmount -e localhost`

**BLOCKED:** docker, apt, systemctl stop/start, zfs write ops, rm su system dirs

Se richiesto operation blocked:
> "Cannot perform that on nas. Use TrueNAS web UI."

### srv1 (Ubuntu) - Full Access

**ALLOWED:** apt, systemctl, docker, git, file operations

**DANGEROUS (requires confirmation):**
- apt install/remove
- docker rm/rmi
- systemctl restart/stop
- rm -rf
- reboot, firewall changes

**Docker path:** `/docker/`

### mnt1 (Ubuntu) - Full Access

**ALLOWED:** apt, systemctl, docker, git, file operations

**DANGEROUS (requires confirmation):**
- apt install/remove
- docker rm/rmi
- systemctl restart/stop
- rm -rf
- reboot, firewall changes

**Docker path:** `/docker/`

**Note:** Docker su mnt1 usa l'utente `docker` (UID 1001, GID 110) come su srv1.
Se l'utente docker non esiste, eseguire:
```bash
sudo groupadd -g 110 docker
sudo useradd -u 1001 -g 110 -d /home/docker -s /bin/sh docker
sudo usermod -aG docker roberto
```

## Confirmation Template

```
I'm going to [ACTION] on [SERVER].

What this will do: [EXPLANATION]
What this affects: [AFFECTED services]
Duration: [EXPECTED time]

Do you want me to proceed? (yes/no)
```

## Data Directories

- `/data` - Application data, databases, archives (srv1)
- `/data/archives` - File archives (srv1)
- `/docker/` - Docker projects (srv1 e mnt1)

## SMTP Config

- Server: mail.stp.vc (SSL, port 465)
- User: srv1.stp.vc
- Credentials: `~/.config/server/credentials.env`

## Mail Account (admin@stp.vc)

- Username: admin@stp.vc
- Password: 13d*c27,Q1.2
- Incoming Server: mail.stp.vc (IMAP, port 993)
- Outgoing Server: mail.stp.vc (SMTP, port 465)

## Watchtower (srv1 only)

- Runs daily at 3:00 AM
- Auto-updates all containers
- Notifications: admin@stepventure.eu

---
name: servers
description: |
  Server management e SSH workflow. Usare per SSH, gestione srv1/srv2/nas,
  operazioni sistema, log analysis. Include srv1 (Ubuntu), srv2 (Ubuntu), nas (TrueNAS Scale).
---

## Servers

| Server | OS | SSH Alias | Role | Access |
|--------|-----|-----------|------|--------|
| srv1 | Ubuntu | `ssh srv1` | Production server | Full (confirm per dangerous ops) |
| srv2 | Ubuntu | `ssh srv2` | Production server | Full (confirm per dangerous ops) |
| nas | TrueNAS Scale | `ssh nas` | Home NAS | Read-only only |

## SSH Connection

```bash
ssh <server>  # srv1, srv2, o nas
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

### srv1/srv2 (Ubuntu) - Full Access

**ALLOWED:** apt, systemctl, docker, git, file operations

**DANGEROUS (requires confirmation):**
- apt install/remove
- docker rm/rmi
- systemctl restart/stop
- rm -rf
- reboot, firewall changes

## Confirmation Template

```
I'm going to [ACTION] on [SERVER].

What this will do: [EXPLANATION]
What this affects: [AFFECTED services]
Duration: [EXPECTED time]

Do you want me to proceed? (yes/no)
```

## Data Directories

- `/data` - Application data, databases, archives
- `/data/archives` - File archives
- `/docker/` - Docker projects

## SMTP Config

- Server: mail.stp.vc (SSL, port 465)
- User: srv1.stp.vc
- Credentials: ~/.config/server/credentials.env

## Watchtower

- Runs daily at 3:00 AM
- Auto-updates all containers
- Notifications: admin@stepventure.eu
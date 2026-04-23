---
name: master
description: |
  Skill master per la sessione. Contiene istruzioni generali e fa git pull
  all'avvio per aggiornare tutti gli skill. Utilizza gli altri skill quando relevanti.
  Skills disponibili: coding, docker, servers
---

## Auto-Update

All'avvio di ogni sessione, esegui:
```bash
cd ~/.config/roberto_ai && git pull
```

## Skills Disponibili

### coding
**Quando usare:** Per attività di coding, git operations, deploy, modifiche al codice.
**Descrizione:** Convenzioni di sviluppo, git workflow (commit regolari, push dopo ogni attività completata).

### docker
**Quando usare:** Per gestione container Docker, docker-compose, creazione nuovi container.
**Descrizione:** Standards per Docker (directory structure, user UID 1001:110, bind mounts only).

### servers
**Quando usare:** Per SSH, connessioni a srv1/srv2/nas, gestione server, operazioni sistema.
**Descrizione:** Workflow SSH, regole per srv1/srv2/nas (TrueNAS Scale), operazioni pericolose confirmation.

## Regole Generali

1. Usa lo skill appropriato quando inizi un task
2. Dopo ogni attività completata, fai `git add . && git commit -m "描述" && git push`
3. Per SSH, usa `ssh srv1`, `ssh srv2`, `ssh nas`
4. Su nas (TrueNAS): solo operazioni read-only
5. Su srv1/srv2: operazioni full con confirmation per operazioni pericolose
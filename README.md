# Roberto AI Settings

Shared AI agent instructions for OpenCode and Claude Code.

## Struttura

```
skills/
├── master/      # Entry point, auto-pull, references other skills
├── coding/      # Git workflow, convenzioni coding
├── docker/      # Docker standards, container management
└── servers/     # SSH workflow, srv1/srv2/nas management
```

## Utilizzo

Gli skill vengono caricati on-demand. Usa lo skill rilevante per il task corrente.

### Auto-Update

Il master skill esegue `git pull` all'avvio per aggiornare tutti gli skill.

### Skills Disponibili

| Skill | Quando usare |
|-------|--------------|
| master | Sempre per primo, contiene riferimenti |
| coding | Attività di coding, git, deploy |
| docker | Gestione container, docker-compose |
| servers | SSH, gestione server, operazioni sistema |

## Server

- **srv1** - Ubuntu production server
- **srv2** - Ubuntu production server
- **nas** - TrueNAS Scale (read-only)

## Note

- Su srv1/srv2: operazioni pericolose richiedono conferma
- Su nas: solo operazioni read-only
- `/root/.config/opencode` è symlink a `/home/roberto/.config/opencode`
- `/root/.claude` è symlink a `/home/roberto/.claude`
---
name: coding
description: |
  Convenzioni di sviluppo e git workflow. Usare quando si fa coding, git operations,
  deploy di codice, modifiche a repository.
---

## Git Workflow

1. **Commit regolari:** Fai commit frequenti con messaggi descrittivi
2. **Push dopo ogni attività completata:** Dopo ogni task completato, esegui:
   ```bash
   cd ~/.config/roberto_ai && git add . && git commit -m "描述" && git push
   ```
3. **Branch:** Usa branch per feature/testing, merge su main quando pronto

## Convenzioni Code

- Usa indentazione consistente (2 o 4 spaces)
- Commenta codice complesso non ovvio
- Nomina variabili in modo descrittivo
- Evita hardcoded values, usa config/env

## Deploy Workflow

1. Verifica che il codice funziona locally
2. Commit con messaggio descrittivo
3. Push al remote
4. Se su srv1: git pull sul server target
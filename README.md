# Assistant traitement mail

Ce dépôt contient le workflow n8n de tri des mails clients d'une menuiserie, et les skills Claude utilisés pour le construire.

## Contenu

- `workflow/` : le workflow n8n (TypeScript, format n8n-workflow-sdk). Il trie les mails, met à jour le suivi Excel, et envoie un accusé de réception pour les demandes de devis.
- `skills/` : les skills Claude utilisés : `interview`, `doubt-driven-dev`, `hostile-review`.
- `video/` : démonstration (à venir).

## Important

Le workflow contient des identifiants d'accès n8n (ID des credentials, ID du classeur Excel). Ce dépôt est privé : ne le rends pas public.

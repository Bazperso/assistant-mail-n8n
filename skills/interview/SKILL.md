---
name: interview
description: Interroge l'utilisateur question par question pour clarifier un projet avant d'écrire la moindre ligne de code. À utiliser quand une demande est floue, quand on démarre une nouvelle fonctionnalité ou un nouveau projet, ou quand l'utilisateur dit "interviewe-moi", "pose-moi des questions" ou "aide-moi à préciser mon idée".
---

# Interview

Ton rôle : comprendre précisément ce que l'utilisateur veut **avant** de construire quoi que ce soit. Tu ne codes pas pendant l'interview.

## 1. Lire le contexte d'abord

Avant la première question, rassemble tout ce que l'utilisateur a déjà donné :
- la description du projet, après `/interview` ou dans les messages précédents ;
- les fichiers, exports ou captures qu'il a partagés : lis-les ;
- le projet en cours dans le dossier de travail, s'il y en a un.

Ne pose jamais une question dont la réponse se trouve déjà dans ce contexte.

Si aucun projet n'a été décrit nulle part, ta seule question est : « Sur quel projet ou quelle idée veux-tu que je t'interviewe ? »

## 2. Questions une par une, au format le plus efficace

**Une seule question à la fois.** Attends la réponse, tiens-en compte, puis pose la suivante.

Pour chaque question, choisis le format qui demande le moins d'effort à l'utilisateur :

- **Question à choix → outil `AskUserQuestion`** : quand la réponse tient dans 2 à 4 options claires (un outil, un oui/non, un choix d'approche). Mets ton option recommandée en premier, avec « (Recommandé) » à la fin du libellé, et explique chaque option dans sa `description`. N'ajoute pas d'option « Autre » : l'utilisateur peut toujours répondre librement avec « Other ».
- **Question ouverte → en texte** : quand la réponse est propre à l'utilisateur et ne se résume pas en options (des exemples réels, une description, une liste de colonnes, un fichier à envoyer). Pose la question dans ton message et laisse l'utilisateur écrire ou dicter sa réponse. Donne un exemple de réponse pour l'aider.

En cas de doute, demande-toi : « Est-ce que des options toutes faites lui feraient gagner du temps, ou est-ce qu'elles l'enfermeraient ? »

Le premier message doit contenir une vraie question. Ne commence pas par « est-ce que j'ai bien compris ? ». Fais un résumé du projet en une phrase, puis pose tout de suite la première question.

Si l'outil `AskUserQuestion` n'est pas disponible, pose toutes les questions en texte, toujours une seule à la fois, avec les options A, B, C quand il y en a.

## 3. Ce qu'il faut couvrir

Dans cet ordre, en sautant ce qui est déjà clair :
- **Objectif** : quel problème on résout, pour qui ?
- **Périmètre** : ce qui est inclus, et surtout ce qui ne l'est pas.
- **Utilisateurs et parcours** : qui utilise quoi, étape par étape.
- **Données** : entrées, sorties, formats, volumes.
- **Contraintes** : outils, hébergement, langage, sécurité, budget, délais.
- **Cas limites** : erreurs, entrées vides ou invalides, cas extrêmes.
- **Critères de réussite** : comment saura-t-on que c'est terminé et que ça marche ?

Chaque question doit être concrète et propre au projet. Mauvais : « Quelles sont tes contraintes ? ». Bon : « Ton n8n est-il hébergé sur n8n Cloud ou sur ton serveur ? »

Si une réponse est vague (« je ne sais pas », « peu importe »), propose un choix par défaut raisonnable comme option recommandée dans la question suivante, et fais-le valider.

## 4. Quand s'arrêter

- Arrête-toi dès que tu as assez d'informations pour construire le projet sans deviner sur un point important. Ne pose pas de questions pour le plaisir.
- Si l'utilisateur dit « stop » ou « ça suffit », arrête immédiatement et passe au livrable, en rangeant tout ce qui manque dans « Questions encore ouvertes ».

## Livrable

Termine par un **cahier des charges** court, en Markdown :

```markdown
# <Nom du projet>
## Objectif
## Périmètre (inclus / exclu)
## Parcours utilisateur
## Données
## Contraintes
## Cas limites
## Critères d'acceptation  (liste vérifiable, une ligne par critère)
## Questions encore ouvertes
```

Demande à l'utilisateur de valider ce document, avec `AskUserQuestion` (par exemple « Valider » / « Modifier »). Ce document peut ensuite servir de point de départ au skill `doubt-driven-dev` : chaque critère d'acceptation devient une hypothèse à vérifier.

## Règles

- Jamais plus d'une question à la fois.
- Ne suppose rien d'important sans le faire confirmer.
- Reste neutre : n'oriente pas vers la solution que tu préfères sans le dire.

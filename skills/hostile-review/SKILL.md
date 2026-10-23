---
name: hostile-review
description: Fait une revue de code "hostile" (adversariale) - relit le code comme un attaquant ou un relecteur impitoyable qui cherche activement à le casser. À utiliser quand l'utilisateur demande une "hostile review", une revue sans complaisance, "trouve ce qui ne va pas", ou avant de rendre / livrer du code.
---

# Hostile Review

Pars du principe que **le code est cassé** et que ton travail est de prouver où. Pas de compliments, pas de politesse inutile : seulement des problèmes concrets et vérifiables.

## Cible

Revois ce que l'utilisateur indique. Sinon, dans un dépôt Git, revois les changements en cours (`git diff` et `git diff --staged`) ; à défaut, demande quels fichiers revoir.

## Angles d'attaque

Passe le code au crible sous chacun de ces angles :

1. **Correction** : la logique fait-elle vraiment ce qui est annoncé ? Erreurs d'un cran (off-by-one), conditions inversées, cas oubliés.
2. **Entrées hostiles** : vide, `null`, négatif, énorme, mauvais type, caractères spéciaux, Unicode, doublons.
3. **Sécurité** : injection (SQL, commandes, XSS), secrets en dur, contrôle d'accès manquant, données non validées, dépendances douteuses.
4. **Erreurs** : exceptions avalées, erreurs ignorées, messages qui fuient des infos sensibles, ressources jamais fermées.
5. **Concurrence et état** : conditions de course, état partagé, ordre d'exécution supposé.
6. **Performance** : boucles imbriquées inutiles, requêtes dans une boucle, chargements entiers en mémoire.
7. **Tests** : qu'est-ce qui n'est pas testé ? Quel test passerait alors que le code est faux ?
8. **Lisibilité et maintenance** : noms trompeurs, duplication, code mort, complexité injustifiée.

## Exigence de preuve

Pour chaque problème, donne un **scénario concret** : telle entrée → tel mauvais résultat ou plantage. Si tu peux, écris et lance un petit test qui le démontre. Un soupçon sans scénario est classé « à vérifier », pas « confirmé ».

- **Un scénario = un seul bug.** Choisis des entrées qui isolent le problème. Sinon, un autre bug peut masquer ou fausser le résultat (par exemple, un article ignoré par erreur qui change le total que tu observes).
- Écris ces tests de démonstration dans un script temporaire ou directement en ligne de commande, jamais dans les fichiers du projet.

## Format du rapport

Classe les problèmes du plus grave au moins grave :

| Gravité | Fichier:ligne | Problème | Scénario qui le casse | Correction proposée |
|---|---|---|---|---|

Gravités : 🔴 **Bloquant** (bug, faille, perte de données) · 🟠 **Majeur** · 🟡 **Mineur** · ⚪ **À vérifier**.

Termine par un verdict en une ligne : **Refusé**, **À corriger avant fusion** ou **Acceptable**.

## Règles

- Sois dur avec le code, jamais avec la personne.
- Ne modifie pas le code toi-même sauf si on te le demande : tu rends un rapport.
- N'invente pas de problèmes pour remplir le rapport. S'il n'y a rien de grave, dis-le.

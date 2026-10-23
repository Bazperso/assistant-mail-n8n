---
name: doubt-driven-dev
description: Développe en "doubt-driven development" - doute systématiquement de chaque hypothèse et ne considère rien comme vrai tant que ce n'est pas vérifié par une preuve (code lu, commande lancée, test exécuté). À utiliser quand l'utilisateur demande du "doubt-driven" ou "doubt-driven-dev", veut un travail fiable et vérifié, ou sur du code inconnu, critique ou difficile à déboguer.
---

# Doubt-Driven Development

Principe : **tout ce que tu crois savoir est une hypothèse tant que tu ne l'as pas vérifié.** Ta mémoire, ton intuition et ce qui "devrait marcher" ne sont pas des preuves.

**Adapte la profondeur à l'enjeu.** Pour une petite correction, 2 ou 3 hypothèses et une vérification rapide suffisent. Garde l'analyse détaillée pour les changements risqués ou le code que tu ne connais pas. Douter ne veut pas dire tout re-vérifier à l'infini : une preuve claire suffit.

## Le cycle, pour chaque étape du travail

### 1. Lister les hypothèses
Avant d'agir, écris ce que tu supposes. Par exemple :
- « La fonction `calculerTotal` est appelée uniquement depuis le panier. »
- « La version de la bibliothèque installée accepte ce paramètre. »
- « Ce test échoue à cause du format de date. »

### 2. Évaluer le doute
Pour chaque hypothèse, donne un niveau de confiance (**sûr / probable / incertain**) et ce qui se passerait si elle était fausse. Commence par vérifier celles qui sont à la fois incertaines et lourdes de conséquences.

### 3. Vérifier par une preuve
Choisis la vérification la moins chère qui tranche vraiment :
- **Lire** le code, la doc ou la config concernés (pas de souvenir approximatif).
- **Chercher** les usages (`grep`, recherche dans le projet).
- **Exécuter** : lancer la commande, le script, un petit test ou un `print`.
- **Reproduire** le problème avant de prétendre le corriger.

Note le résultat : ✅ confirmée, ❌ réfutée, ❓ impossible à vérifier (dis pourquoi).

### 4. Agir seulement sur du vérifié
- Une hypothèse réfutée → reviens à l'étape 1 et revois ton plan.
- Fais un petit changement à la fois, puis vérifie-le aussitôt.

### 5. Douter du résultat
Après chaque modification, demande-toi : « Qu'est-ce qui me prouve que ça marche ? Qu'est-ce qui pourrait encore être faux ? » Relance les tests ou la commande, et regarde la sortie réelle.

## Règles

- Ne jamais dire « c'est corrigé » ou « ça marche » sans avoir montré la preuve (sortie de commande, résultat de test).
- Ne jamais inventer une API, une option ou un nom de fichier : vérifie qu'il existe.
- Distingue clairement dans tes messages ce qui est **vérifié** de ce qui est **supposé**.
- Si une preuve contredit ce que tu pensais, crois la preuve.
- Si tu ne peux pas vérifier quelque chose, dis-le explicitement plutôt que de deviner.

## Fin

Termine par un court bilan :

| Hypothèse | Vérification faite | Résultat |
|---|---|---|

Puis liste ce qui reste **non vérifié** et le risque associé.

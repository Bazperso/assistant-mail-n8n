# Skills Claude

Trois skills utilisés pour concevoir et fiabiliser ce projet. Chacun est un fichier `SKILL.md`, lisible par Claude Code.

| Skill | Ce qu'il fait | Quand l'utiliser |
|---|---|---|
| [`interview`](interview/SKILL.md) | Pose les questions **une par une** pour clarifier un projet avant d'écrire la moindre ligne de code. | Quand une demande est floue, ou avant de démarrer un projet. |
| [`doubt-driven-dev`](doubt-driven-dev/SKILL.md) | Considère chaque hypothèse comme fausse tant qu'elle n'est pas vérifiée par une preuve (code lu, commande lancée, test exécuté). | Sur du code critique, inconnu, ou difficile à déboguer. |
| [`hostile-review`](hostile-review/SKILL.md) | Relit le code comme un attaquant ou un relecteur sans complaisance, pour trouver ce qui peut casser. | Avant de livrer du code, ou pour une revue sans concession. |

## Ordre conseillé

1. **`interview`** — définir le besoin.
2. **`doubt-driven-dev`** — construire en vérifiant chaque étape.
3. **`hostile-review`** — relire avant de livrer.

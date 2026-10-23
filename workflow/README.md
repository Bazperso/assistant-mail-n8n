# Workflow — FINAL WORKFLOW AVEC NOTES

Ce dossier contient le workflow **n8n** complet : [`FINAL WORKFLOW AVEC NOTES.workflow.ts`](FINAL%20WORKFLOW%20AVEC%20NOTES.workflow.ts), écrit avec le SDK `@n8n/workflow-sdk`.

![Vue d'ensemble du workflow](images/workflow.webp)

---

## Déroulé pas à pas

### 1. 📥 Nouveau mail reçu
Déclencheur **Microsoft Outlook** : vérifie la boîte pro chaque minute et démarre le workflow pour chaque nouveau mail.

### 2. 🧹 Ignorer les mails déjà traités
Mémorise les identifiants des mails déjà passés, pour ne jamais traiter deux fois le même mail.

### 3. 🤖 Analyse du mail par l'IA
**Google Gemini** lit l'expéditeur, l'objet et le contenu, puis renvoie un objet JSON :

| Champ | Rôle |
|---|---|
| `est_client` | Vrai si l'expéditeur est un client ou un client potentiel |
| `nom`, `email`, `telephone` | Coordonnées (l'adresse de l'expéditeur sert de repli) |
| `categorie` | Nouvelle demande, Devis en attente, Devis signé, Dossier en cours, Facturation, Réclamation / SAV |
| `resume` | Une phrase qui résume la demande |
| `urgent` | Vrai seulement si le ton ou le contenu l'exige |
| `action` | `accuse_devis`, `brouillon` ou `aucune` |

Les pubs, newsletters, fournisseurs et mails internes ne sont **pas** considérés comme des clients.

### 4. 🧾 Extraire les infos client
Transforme la réponse de l'IA en champs exploitables pour la suite du workflow.

### 5. 🔀 Mail client ?
Garde uniquement les clients. Les adresses `noreply` et `no-reply` sont exclues.

### 6. 📊 Mettre à jour le suivi Excel
Écrit dans la feuille `Feuil1` :
- **sans doublon** : la ligne est recherchée par adresse mail, et mise à jour si elle existe ;
- avec la date, le nom, les coordonnées, la catégorie, le résumé, l'urgence, l'action choisie par l'IA et l'identifiant du mail.

### 7. 🧭 Choisir la réponse
Aiguille selon `action` :
- `accuse_devis` → branche de l'accusé de réception ;
- `brouillon` → branche de brouillon *(en attente de validation)* ;
- `aucune` → rien ne se passe.

### 8. ✉️ Accuser réception du devis
Répond **dans le fil du mail d'origine** avec un texte fixe : la demande a bien été reçue et sera traitée rapidement. C'est le seul envoi automatique du workflow.

---

## Ce qui n'est pas encore dans cette version

Ces briques existent dans les versions précédentes, mais n'ont pas encore été validées de bout en bout. Elles seront ajoutées une à une :

- **Brouillon de réponse** pour les autres mails clients (à relire avant envoi).
- **Pièces jointes** : enregistrement du nom des fichiers par client.
- **Relance hebdomadaire** des devis sans réponse depuis 7 jours.
- **Alerte urgence** : marquage en rouge des devis non traités après 24 h.
- **Demande d'avis Google** : brouillon après facturation.

---

## Prérequis

- Un compte **Microsoft 365** avec Outlook et Excel (OneDrive).
- Un compte **Google AI Studio** pour la clé Gemini.
- Les credentials suivants configurés dans n8n :
  - `Excel - Suivi clients` (Microsoft Excel OAuth2)
  - `Outlook - Boîte pro` (Microsoft Outlook OAuth2)
  - `Gemini - Analyse des mails` (Google Gemini PaLM API)

## Avant d'activer

1. Ajouter dans `Feuil1` les colonnes `REPONSE AUTO`, `ID MAIL`, `RELANCE` et `AVIS`.
2. Créer la feuille `Pièces jointes`.
3. Lancer une exécution de test avec un mail de demande de devis.
4. Vérifier : accusé reçu, ligne ajoutée dans Excel, aucune erreur dans n8n.
5. Activer le workflow.

> ⚠️ Ce workflow envoie de vrais mails. Ne l'active qu'une fois les tests concluants, et ne l'exécute pas avec une boîte contenant des clients réels sans l'avoir relu.

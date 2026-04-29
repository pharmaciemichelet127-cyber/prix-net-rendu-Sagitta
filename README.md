# Prix Net Rendu — Pharmacie Michelet

Application web de calcul automatique du **prix net rendu** par produit à partir d'une facture fournisseur.

## Fonctionnement

1. Importez une facture fournisseur (PDF, JPG ou PNG)
2. Claude analyse le document et extrait automatiquement :
   - Tous les produits (désignation, EAN, référence, quantité, prix unitaire HT)
   - Tous les frais annexes présents sur la facture (transport, douane, port, assurance…)
3. Les frais sont répartis **au prorata du montant HT de chaque ligne**
4. Le **prix net rendu unitaire** est calculé et affiché pour chaque produit

## Formule de calcul

```
frais_ligne   = total_frais × (total_ht_ligne / total_ht_produits)
net_rendu_u   = (total_ht_ligne + frais_ligne) / quantité
```

## Installation

### 1. Cloner le repo

```bash
git clone https://github.com/VOTRE_PSEUDO/prix-net-rendu.git
cd prix-net-rendu
```

### 2. Configurer la clé API

Dans `index.html`, remplacez la valeur de `API_KEY` :

```javascript
const API_KEY = 'sk-ant-api03-VOTRE_CLE_ICI';
```

> **Important** : ne committez jamais votre clé API. Ajoutez une ligne `*.env` dans `.gitignore` si vous souhaitez externaliser la clé.

### 3. Lancer localement

Ouvrez simplement `index.html` dans votre navigateur. Aucun serveur requis.

Ou avec un serveur local :

```bash
npx serve .
# puis ouvrez http://localhost:3000
```

## Déploiement sur Vercel

1. Connectez le repo sur [vercel.com](https://vercel.com)
2. Framework preset : **Other**
3. Déployez — aucune variable d'environnement à configurer côté Vercel

> La clé API est embarquée dans le HTML. Pour un déploiement plus sécurisé, envisagez un backend proxy (ex. Vercel Serverless Functions) qui stocke la clé dans une variable d'environnement Vercel.

## Formats supportés

| Format | Extension |
|--------|-----------|
| PDF    | `.pdf`    |
| Image JPEG | `.jpg`, `.jpeg` |
| Image PNG  | `.png` |

## Stack technique

- HTML / CSS / JavaScript vanilla — aucune dépendance
- API Anthropic Claude (`claude-sonnet-4-20250514`) pour l'extraction et l'analyse
- Google Fonts (DM Sans, DM Mono, Instrument Serif)

## Projet lié

Ce module fait partie de l'écosystème **ReconcilIA** de la Pharmacie Michelet.  
Voir : [github.com/pharmaciemichelet127-cyber/Reconcilia](https://github.com/pharmaciemichelet127-cyber/Reconcilia)

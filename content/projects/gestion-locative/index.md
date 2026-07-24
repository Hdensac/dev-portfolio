---
title: "Gestion Locative - Plateforme de Gestion de Biens Immobiliers"
date: 2026-07-24
summary: "Application web full-stack de gestion locative multi-propriétaires avec suivi des loyers, génération automatique de quittances PDF et tableau de bord analytique"
tags:
  - Full-Stack
  - Django
  - Gestion Immobiliere
  - PDF Generation
  - Multi-tenant
tech_stack:
  - Django 6.0
  - Python
  - SQLite / PostgreSQL
  - Cloudinary
  - ReportLab
  - WhiteNoise
  - Render
featured: true
---

Gestion Locative est une plateforme web complète conçue pour aider plusieurs propriétaires à gérer leurs maisons, chambres, locataires, loyers et quittances depuis une interface centralisée.

## Apercu

Le projet est né d'un besoin concret: remplacer les tableaux Excel et les carnets papier par un outil web structuré, accessible depuis n'importe quel navigateur, avec génération automatique de documents PDF professionnels.

L'application est pensée pour un contexte francophone et local, avec interface en français, gestion multi-propriétaires stricte et déploiement cloud-ready.

## Fonctionnalites

### Gestion du parc immobilier
- Création, modification et suppression des maisons avec adresse et description
- Gestion des chambres par maison avec numérotation unique et statut occupé/libre
- Calcul automatique du taux d'occupation par maison et globalement
- Vue détaillée de chaque maison avec la liste des chambres et occupants actuels

### Gestion des locataires
- Fiche locataire complète avec nom, téléphone, email, chambre assignée et dates d'entrée/sortie
- Suivi de la caution avec mode de paiement, date et reçu PDF
- Statut actif/sorti avec archivage des anciens locataires
- Recherche multi-critères par nom, téléphone ou email

### Suivi des paiements
- Enregistrement des paiements avec mois concerné, montant, date et mode de paiement
- Paiement rapide sans affectation immédiate de mois
- Affectation ultérieure d'un paiement rapide à un mois précis
- Blocage métier si un paiement rapide non affecté existe déjà pour un locataire

### Quittances PDF automatiques
- Génération automatique d'une quittance PDF à chaque paiement complet via un signal Django `post_save`
- Numérotation unique de type `QUIT-YYYY-ID_PAIEMENT`
- Stockage local en développement et sur Cloudinary en production
- Mise en page professionnelle avec logo dynamique, signature numérique et format A5

### Tableau de bord et rapports
- Vue synthétique propriétaire avec loyers encaissés, impayés et taux d'occupation
- Tableau de bord super-admin avec statistiques globales
- Détection intelligente des impayés selon un mois de référence
- Export PDF des rapports mensuels par propriétaire, globalement et par maison

## Implémentation technique

### Modèle de données

```text
Maison --> Chambre --> Locataire --> Paiement --> Quittance
  |                           |
  +--> proprietaire (User)     +--> mois_concerne / date_paiement
```

Le modèle `Locataire` expose une méthode `get_retards_details(reference_date)` qui calcule les mois impayés en parcourant l'historique des paiements.

### Logique des impayes

```python
def _get_mois_reference(today):
    if today.day < 30:
        return (today.replace(day=1) - timedelta(days=1)).replace(day=1)
    return today.replace(day=1)
```

Cette règle évite de considérer un locataire en retard trop tôt dans le mois.

### Generation PDF

- Quittances A5 rendues directement avec `ReportLab`
- Rapports A4 avec tableaux structurés
- Logo dynamique basé sur les initiales du propriétaire
- Signature numérique intégrée automatiquement en bas de la quittance

### Deploiement

| Composant | Développement | Production |
| --- | --- | --- |
| Base de données | SQLite | PostgreSQL |
| Fichiers médias | Local | Cloudinary |
| Fichiers statiques | Django dev server | WhiteNoise |
| Secrets | `.env` local | Variables d'environnement |

## Tests automatises

La suite de tests couvre les cas critiques:

- Détection des trous dans l'historique des paiements
- Mois de référence et exigibilité des loyers
- Paiements rapides non affectés et blocage de doublon
- Génération et numérotation unique des quittances
- Affectation de mois a posteriori avec création de quittance

## Points forts

- Logique métier robuste pour les cas limites
- Documents PDF de qualité professionnelle
- Architecture multi-tenant propre
- Déploiement cloud-ready
- Interface en français adaptée au contexte local

<div align="center">

<img src="https://img.shields.io/badge/Python-3.10+-3776AB?style=flat-square&logo=python&logoColor=white"/>
<img src="https://img.shields.io/badge/pandas-2.0-150458?style=flat-square&logo=pandas&logoColor=white"/>
<img src="https://img.shields.io/badge/matplotlib-seaborn-11557C?style=flat-square"/>
<img src="https://img.shields.io/badge/Status-Portfolio--Ready-2a5c45?style=flat-square"/>

<br/><br/>

# **AFRIMARKET**
# Analyse Stratégique des Données E-Commerce

### *Juillet – Décembre 2025 · 8 villes · 4 catégories · 9 400 commandes*

<br/>

> "AfriMarket ne souffre pas d'un problème de modèle.
> Elle souffre de quelques fuites précises — et cette analyse les localise toutes."

<br/>

</div>

## Table des matières

- [Contexte business](#-contexte-business)
- [Ce que révèle l'analyse](#-ce-que-révèle-lanalyse)
- [Structure du projet](#-structure-du-projet)
- [Installation & utilisation](#-installation--utilisation)
- [Méthodologie complète](#-méthodologie-complète)
- [Résultats clés](#-résultats-clés)
- [Les 5 recommandations](#-les-5-recommandations-stratégiques)
- [Stack technique](#-stack-technique)
- DAVID SOUWAN (#-auteur)


## 🌍 Contexte business

AfriMarket est une entreprise e-commerce panafricaine opérant dans 8 grandes villes d'Afrique francophone (Kinshasa, Abidjan, Douala, Dakar, Lomé, Cotonou, Libreville, Brazzaville). Elle commercialise des produits dans 4 catégories : Électronique, Mode, Maison, Beauté.

La direction a constaté des signaux préoccupants sans en comprendre les causes :

| Signal | Symptôme observé |
|---|---|
| 📉 Variations CA | Oscillations de ±8% mensuelles inexpliquées |
| 🔄 Taux de retour | "Préoccupant sur certains produits" |
| 💸 Budget marketing | Dépenses élevées, ROI non mesuré |
| 🗺️ Géographie | Performances très variables selon les villes |

Mission : Produire une analyse stratégique complète permettant à la direction de prendre des décisions actionnables.


## 💡 Ce que révèle l'analyse

Cinq constats ont émergé des données. Classés par urgence :

🔴 CRITIQUE   │ Électronique : 13,84% de retours (norme = 3-5%)
🔴 URGENT     │ Douala : 12,92% d'annulations (vs 0% ailleurs)
🟡 FUITE      │ Beauté : seule catégorie déficitaire (profit = -380 USD)
🟢 OPPORTUNITÉ│ Email Marketing : ROI 231x avec seulement 3,4% du budget
🟢 LEVIER     │ 608 clients Fidèles = 78,5% du CA — zone de conversion prioritaire

## 📁 Structure du projet

afrimarket-analysis/
│
├── 📓 AfriMarket_Analyse_Strategique.ipynb   ← Notebook principal (16 sections)
│
├── 📂 data/
│   └── afrimarket_dataset_senior.csv         ← Dataset brut (10 100 lignes)
│
├── 📂 outputs/
│   ├── viz1_ca_categorie.png                 ← CA par catégorie + profit + retours
│   ├── viz2_villes.png                       ← Performance financière par ville
│   ├── viz3_roi_marketing.png                ← ROI par canal marketing
│   ├── viz4_evolution.png                    ← Évolution mensuelle CA + profit
│   ├── viz5_clients.png                      ← Segmentation clients (3 groupes)
│   └── viz6_heatmap_retours.png              ← Heatmap retours catégorie × ville
│
├── 📄 README.md                              ← Ce fichier
└── 📄 rapport.html                       ← Dépendances Python

## ⚙️ Installation & utilisation

### Prérequis

Python 3.10+
pip
### Installation
# 1. Cloner le dépôt
git clone https://github.com/votre-username/afrimarket-analysis.git
cd afrimarket-analysis

# 2. Installer les dépendances
pip install -r requirements.txt

# 3. Placer le fichier de données
cp afrimarket_dataset_senior.csv data/

# 4. Lancer Jupyter
jupyter notebook AfriMarket_Analyse_Strategique.ipynb
### requirements.txt

pandas>=2.0.0
numpy>=1.24.0
matplotlib>=3.7.0
seaborn>=0.12.0
jupyter>=1.0.0
### Exécution complète

# Dans VS Code avec l'extension Jupyter :
# Ouvrir le .ipynb → Run All (Ctrl+Shift+Enter)
# Les 6 visualisations se sauvegardent automatiquement dans outputs/
---

## 🔬 Méthodologie complète

### Phase 1 — Audit des données

Avant nettoyage : 10 100 lignes × 14 colonnes

Anomalies détectées :
├── Doublons exacts          : 100 lignes  (1,0%)
├── Quantités = 0            : 608 lignes  (6,0%)
├── Prix négatifs            : 632 lignes  (6,3%)
├── Remises négatives        : 614 lignes  (6,1%)
├── Encodage UTF-8 corrompu  : ~45% des lignes (catégories, villes, statuts)
└── Orthographe ville        : 'Kinshassa' → 'Kinshasa' (605 lignes)
### Phase 2 — Data Cleaning

# Corrections appliquées (dans l'ordre)
1. Correction encodage UTF-8  →  mapping dictionnaire exact
2. Suppression doublons       →  drop_duplicates()
3. Remises négatives          →  abs()  [pas 0 — info préservée]
4. Prix négatifs              →  médiane par catégorie  [pas abs()]
5. Quantités nulles           →  suppression  [pas remplacement par 1]
6. Standardisation dates      →  pd.to_datetime()

Après nettoyage : 9 400 lignes  (93% des données conservées)
> Principe directeur : Corriger sans inventer. Supprimer uniquement ce qui est structurellement invalide.

### Phase 3 — Feature Engineering

| Variable créée | Formule | Usage analytique |
|---|---|---|
| chiffre_affaires | prix × quantite × (1 - remise) | Revenu réel par transaction |
| marge_brute | CA × 0.30 | Rentabilité avant coûts |
| profit_net | marge - cout_marketing - cout_livraison | Rentabilité nette réelle |
| indicateur_retour | 1 si statut == 'Retournée' | Calcul taux de retour |
| indicateur_annulation | 1 si statut == 'Annulée' | Calcul taux d'annulation |
| nb_commandes_client | groupby id_client | Mesure de fidélité |
| clv_totale | sum(CA) par client | Customer Lifetime Value |
| segment_client | Nouveau / Régulier / Fidèle | Segmentation RFM simplifiée |

### Phase 4 — Analyses (5 dimensions)

✅ Performance globale     → KPIs : CA, profit, panier, taux retour/annulation
✅ Analyse par catégorie   → CA, marge, profit, taux retour, évolution mensuelle
✅ Analyse géographique    → CA, profit, annulations par ville + croissance
✅ Analyse marketing       → CA par canal, ROI, part de budget, optimisation
✅ Analyse clients         → Segmentation, Pareto 80/20, top 10, CLV, rétention

## 📊 Résultats clés

### Performance globale

┌─────────────────────────────────────────────────┐
│  AFRIMARKET · JUILLET – DÉCEMBRE 2025           │
├─────────────────────────────────────────────────┤
│  CA total           :    2 557 014 USD         │
│  Marge brute (30%)  :      767 104 USD         │
│  Profit net         :      641 153 USD  ✓      │
│  Marge nette        :           25,1%           │
│  Panier moyen       :          272 USD         │
│  Taux de retour     :          8,14%  ⚠️        │
│  Taux d'annulation  :          1,95%            │
│  Clients uniques    :          1 747            │
│  Clients récurrents :           74%   ✓         │
└─────────────────────────────────────────────────┘
### Par catégorie

| Catégorie | CA | Part | Profit % | Taux retour | Signal |
|---|---|---|---|---|---|
| Électronique | 1 906 545 | 74,6% | 27,9% | 13,84% | 🔴 |
| Maison | 382 768 | 15,0% | 23,7% | 4,95% | 🟢 |
| Mode | 189 633 | 7,4% | 10,0% | 7,44% | 🟡 |
| Beauté | 78 069 | 3,1% | -0,5% | 2,79% | 🔴 |

### Par canal marketing
| Canal | ROI | Budget | CA généré | Verdict |
|---|---|---|---|---|
| Email | 231x | 3,4% | 545 585 | 🟢 Sous-financé |
| Google Ads | 50x | 18,9% | 675 026 | 🟢 Efficace |
| Instagram Ads | 25x | 54,2% | 966 448 | 🔴 Sur-financé |
| Influenceur | 22x | 23,5% | 369 955 | 🟡 À optimiser |

### Segmentation clients

                    Nb clients    CA moyen     Part du CA
                    ──────────    ────────     ──────────
  Fidèle (4+ cmd)  │   608    │  3 307 USD  │  78,5%  │ ◄── Le vrai moteur
  Régulier (2-3)   │   685    │    625 USD  │  16,8%  │ ◄── Zone de conversion
  Nouveau (1 cmd)  │   454    │    260 USD  │   4,6%  │

  Un client Fidèle vaut 12,7x un client Nouveau.
### Évolution mensuelle

Juil  │████████████████████░░  401k  (base)
Août  │██████████████████████░  437k  +8,8%  ↑
Sept  │████████████████████░░░  404k  -6,6%  ↓
Oct   │█████████████████████░░  435k  +6,6%  ↑
Nov   │████████████████████░░░  401k  -7,9%  ↓
Déc   │████████████████████████ 472k  +17,8% ↑  ← Pic saisonnier
---

## 🎯 Les 5 recommandations stratégiques

### P1 — Résoudre la logistique Douala ⚡ *0–1 mois*

Problème : 12,92% d'annulations à Douala contre 0% dans toutes les autres villes.
Action : Audit du prestataire livraison local → renégociation ou changement.
KPI : Taux annulation Douala < 3% · ROI estimé : >300%

---

### P2 — Multiplier le budget Email par 4 ⚡ *0–3 mois*

Problème : ROI 231x avec 3,4% du budget (vs Instagram : ROI 25x avec 54%).
Action : Budget 2 349 → 9 000 USD · 3 séquences automatisées (relance, fidélité, panier abandonné).
KPI : CA Email > 25% du total · Projection : +720 000 USD à ROI 80x conservateur

---

### P3 — Auditer les retours Électronique 📋 *0–2 mois*

Problème : 13,84% de retours sur 74,6% du CA = ~286 000 USD de CA perdu.
Action : Analyse des 491 retours · Amélioration fiches produits · Audit fournisseurs.
KPI : Taux retour Électronique < 8% en 3 mois · CA récupérable : ~120 000 USD

---

### P4 — Fixer Beauté ou l'arrêter 🔧 *1–2 mois*

Problème : Seule catégorie déficitaire. Panier 44 USD vs coûts fixes ~12 USD.
Action A : Panier minimum 3 500 USD + bundling.
Action B : Suspension → réallocation vers Maison (profit 23,7%).
KPI : Profit Beauté > 0 sous 60 jours

---

### P5 — Programme conversion Régulier → Fidèle 📈 *2–5 mois*

Problème : 685 Réguliers à 625 USD vs Fidèles à 3 307 USD. Écart de 5,3x.
Action : Offre automatique à la 3ème commande · Séquence Email 4 semaines.
KPI : 200 conversions · Impact : +536 400 USD sans acquisition

---

## 🛠️ Stack technique

# Core
pandas      == 2.0+    # Manipulation et analyse de données
numpy       == 1.24+   # Calculs numériques
matplotlib  == 3.7+    # Visualisations customisées
seaborn     == 0.12+   # Visualisations statistiques

# Environment
Python      == 3.10+
Jupyter     == 1.0+
VS Code     + Extension Jupyter
---


## ⚠️ Limites de l'analyse

- La marge brute à 30% est une hypothèse d'estimation — les marges réelles par produit sont inconnues
- Le profit_net exclut les coûts fixes (loyer, salaires, infrastructure)
- La CLV est calculée sur 6 mois seulement — non représentative de la valeur long terme
- Le taux de retour par ville × catégorie est basé sur des volumes parfois faibles (intervalles de confiance larges)
- Les données de Décembre 2025 peuvent contenir un biais saisonnier de fin d'année

---

## 📈 Ce projet en chiffres

10 100  lignes brutes analysées
   708  lignes invalides supprimées (7%)
 9 400  commandes nettoyées et analysées
     8  nouvelles variables créées (feature engineering)
     6  visualisations professionnelles produites
     5  recommandations stratégiques chiffrées
     3  IA mobilisées en workflow structuré
---

## 👤 Auteur

DAVID SOUWAN · Data Analyst


<div align="center">

*Projet réalisé dans le cadre d'une formation Data Analytics*
*Méthodologie : Audit → Nettoyage → Feature Engineering → Analyse → Recommandations*
*Stack : Python · pandas · matplotlib · seaborn*

<br/>

⭐ Si ce projet vous a été utile, une étoile GitHub est appréciée.

</div>

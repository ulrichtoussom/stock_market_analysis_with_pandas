 # Analyse de portefeuilles boursiers avec pandas

Analyse exploratoire de **3 000 transactions boursières** (achats/ventes) réparties sur 3 portefeuilles et 15 titres, croisées avec **14 625 cours de clôture quotidiens** (janvier 2023 – septembre 2026), afin de mesurer l'activité de trading, la performance des titres et la plus-value latente de chaque position.

> ⚠️ Les données sont **synthétiques** (entreprises et tickers fictifs). Le projet a été réalisé dans le cadre d'une formation Python.

## Objectifs

- Nettoyer un jeu de données financier comportant des valeurs manquantes
- Calculer les montants réels des opérations en tenant compte des frais de courtage
- Identifier les secteurs, titres et portefeuilles les plus actifs
- Analyser l'évolution de l'activité dans le temps
- Calculer la position nette et la plus-value latente de chaque titre
- Produire un rapport synthétique exportable

## Données

| Fichier | Lignes | Contenu |
|---|---|---|
| `transactions.csv` | 3 000 | date, entreprise, ticker, secteur, type d'opération, quantité, prix unitaire, frais, portefeuille |
| `historique_cours.csv` | 14 625 | cours de clôture quotidien des 15 titres (jours ouvrés) |

## Démarche

1. **Exploration et qualité des données** : structure, types, statistiques descriptives, détection de 20 prix manquants.
2. **Nettoyage** : imputation des prix manquants par la moyenne du même ticker, puis **reconstitution exacte** à partir de l'historique des cours (après avoir vérifié que le prix de transaction correspond toujours au cours de clôture du jour).
3. **Variables calculées** : montant brut, montant net (frais ajoutés à l'achat, déduits à la vente), quantité signée.
4. **Agrégations** : volumes par secteur, titre et portefeuille (`groupby`, `agg`, `pivot_table`), solde net achats/ventes.
5. **Analyse temporelle** : montants par année et par mois, comparaison via le **montant mensuel moyen** pour ne pas biaiser la comparaison avec l'année 2026 incomplète.
6. **Fusion de sources** (`merge`) : position nette + prix d'achat moyen + dernier cours → plus-value latente par titre.
7. **Performance des titres** sur la période et cours moyen par secteur et par année.
8. **Export** d'un rapport sectoriel en CSV.

## Principaux résultats

- **Technologie** et **Finance** concentrent le plus gros volume échangé (≈ 9,2 M et 7,7 M).
- Les 3 portefeuilles sont **acheteurs nets** sur la période (solde net de −1,5 M à −1,8 M).
- L'activité mensuelle moyenne progresse de 2023 à 2025 (≈ 650 k → 875 k), puis recule légèrement en 2026.
- Meilleure performance : **ORA (+145 %)** ; plus forte baisse : **DYN (−25 %)**.
- Plus grosse plus-value latente : **GAM (≈ +356 k)** ; plus grosse moins-value : **NOV (≈ −69 k)**.

## Limites et pistes d'amélioration

- Prix d'achat moyen calculé en moyenne simple : une **moyenne pondérée par les quantités** serait plus juste.
- Les positions nettes négatives (plus de ventes que d'achats sur la période) s'expliquent probablement par des titres détenus avant 2023 : une méthode de calcul FIFO ou PRU serait plus rigoureuse.
- Ajout de visualisations (matplotlib / seaborn) et application à des données réelles (ex. `yfinance`).

## Technologies

Python · pandas · NumPy · Jupyter Notebook

## Lancer le projet

```bash
pip install pandas numpy jupyter
jupyter notebook analyse_portefeuilles.ipynb
```
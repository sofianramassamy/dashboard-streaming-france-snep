# dashboard-streaming-france-snep
# 🎵 Dashboard Power BI / Looker Studio Le marché français de la musique enregistrée (2019-2025) — Analyse des données SNEP
> **En six ans, le streaming a fait basculer une industrie : porteur à lui seul de la croissance d'un marché qui franchit le milliard d'euros en 2024, il est passé de la moitié aux deux tiers des revenus de la musique enregistrée en France.**

📊 Projet de data analyse réalisé avec **Google Sheets**, **Looker Studio** et **Power BI**, à partir des bilans annuels du SNEP.

---

## 🎯 Objectif

Répondre à une question simple en apparence : **qu'est-ce qui fait réellement croître le marché français de la musique enregistrée depuis 2019 ?**

Le dashboard décompose le chiffre d'affaires du marché en quatre segments (streaming, ventes physiques, synchronisation, droits voisins) pour identifier le moteur de la croissance, quantifier son poids, et visualiser la recomposition du marché entre 2019 et 2025.

---

## 📊 Résultats clés

- **+38,7 %** de croissance du CA total du marché entre 2019 et 2025 (772 M€ → 1 071 M€), avec le **franchissement du milliard d'euros dès 2024**.
- **+90,7 %** de croissance du CA streaming sur la même période (368,3 M€ → 702,2 M€) : le streaming porte à lui seul la quasi-totalité de la croissance du marché.
- La **part du streaming** passe d'environ la moitié du marché en 2019 à **65,6 % en 2025** — soit près des deux tiers des revenus.
- Les autres segments stagnent ou reculent : le physique se stabilise autour de 200 M€, les droits voisins autour de 120 M€, la synchro reste marginale (~35 M€).

---

## 🔗 Dashboard interactif

👉 **[Consulter le dashboard Looker Studio (lien public)](https://lookerstudio.google.com/VOTRE_LIEN_ICI)**

Le rapport Power BI (`.pbix`) est également disponible dans ce dépôt, avec des captures d'écran des deux versions dans le dossier du projet.

---

## 🛠️ Démarche et outils

Pipeline en **5 étapes**, de la donnée brute au dashboard :

1. **Collecte** — Extraction manuelle des chiffres depuis les 7 bilans annuels du SNEP (2019 à 2025), publiés en PDF, avec traçabilité de la source pour chaque année.
2. **Structuration** — Construction d'une table propre dans **Google Sheets** : une ligne par année, une colonne par segment de CA (streaming, physique, synchro, droits voisins), calculs de parts et de taux de croissance.
3. **Prototypage** — Première visualisation dans **Looker Studio** (connecté à Google Sheets) : courbes d'évolution, barres empilées en valeur et en %, dashboard partageable publiquement.
4. **Modélisation** — Reconstruction dans **Power BI** avec des **mesures DAX** : `CALCULATE` pour filtrer les années de référence, `DIVIDE` pour sécuriser les ratios (parts et taux de croissance), et le pattern `VAR` / `RETURN` pour des mesures lisibles et maintenables.
5. **Design & storytelling** — Mise en page des deux dashboards Power BI (évolutions + proportions), cartes KPI, titre-message, et vérification de cohérence entre les trois outils.

**Stack :** Google Sheets · Looker Studio · Power BI (DAX)

---

## ⚠️ Défis rencontrés

C'est souvent la partie la plus formatrice du projet :

- **« Numérique » ≠ « streaming »** — Dans les bilans SNEP, le périmètre « numérique » inclut aussi le téléchargement. Il a fallu isoler rigoureusement le CA *streaming* seul pour chaque année, afin de ne pas gonfler artificiellement sa croissance et de comparer des périmètres identiques sur toute la période.
- **Des chiffres révisés d'un bilan à l'autre** — Une même année peut afficher des valeurs légèrement différentes selon le bilan consulté (révisions a posteriori du SNEP). Règle adoptée : retenir le bilan le plus récent qui mentionne l'année, et documenter la source de chaque ligne dans le fichier de données.
- **Le piège du double axe** — Comparer le streaming (~700 M€) et la synchro (~35 M€) sur un même graphique invite à utiliser un double axe… qui déforme la lecture et suggère de fausses convergences. Choix final : un axe unique, quitte à assumer l'écart d'échelle, car c'est précisément lui qui raconte l'histoire.
- **Sanity check des arrondis** — La somme des segments ne retombe pas toujours exactement sur le CA total publié (arrondis du SNEP). Un contrôle systématique des écarts a été mis en place pour distinguer un simple arrondi d'une véritable erreur de saisie.

---

## 🚀 Limites et pistes d'amélioration

- **Mesures DAX à dynamiser** — Les années de référence (2019, 2025) sont actuellement codées en dur dans certaines mesures. Piste : les rendre dynamiques avec `MAX()` / `MIN()` sur la colonne année, pour que les KPI se mettent à jour automatiquement à chaque nouvelle année de données.
- **Mise à jour annuelle** — Intégration du bilan SNEP 2026 dès sa publication, sans modification de la structure du modèle.
- **Enrichissements possibles** — Distinguer streaming par abonnement / financé par la publicité, et comparer la trajectoire française aux données internationales (IFPI).

---

## 📁 Sources

- **SNEP** (Syndicat National de l'Édition Phonographique) — bilans annuels de la production musicale française, éditions **2019 à 2025**.
- Site officiel : [snepmusique.com](https://snepmusique.com)

Chaque ligne du fichier de données (`Donnés_Data_SNEP.xlsx`) référence le bilan exact dont elle est issue.

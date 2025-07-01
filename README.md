# Data-Analyst-project

## Description du Projet

Ce projet d'analyse de données se concentre sur l'exploration d'un ensemble de données e-commerce (similaire à Olist) afin de mieux comprendre les facteurs influençant la satisfaction client et d'identifier les points d'amélioration potentiels dans le processus de livraison.

Les principales questions abordées dans cette analyse sont :
- Quelle est la répartition des scores de satisfaction client ?
- Le délai de livraison a-t-il un impact sur la satisfaction client ?
- Quel est le montant moyen des commandes en fonction du score de satisfaction ?
- Quelles sont les villes et les catégories de produits qui génèrent le plus de retards de livraison ?
- Quel est l'écart moyen entre la date de livraison estimée et la date réelle ?

## Données

L'analyse est basée sur un ensemble de données e-commerce publiques d'Olist, une plateforme de vente en ligne brésilienne. Les données sont réparties dans plusieurs fichiers CSV, représentant différentes entités du système :

- `olist_customers_dataset.csv`: Informations sur les clients.
- `olist_geolocation_dataset.csv`: Données de géolocalisation (codes postaux, latitude, longitude, villes, états).
- `olist_order_items_dataset.csv`: Détails des articles commandés (ID de commande, ID de produit, ID de vendeur, prix, frais de port).
- `olist_order_payments_dataset.csv`: Informations sur les paiements des commandes (type de paiement, nombre de versements, valeur du paiement).
- `olist_order_reviews_dataset.csv`: Avis des clients sur les commandes (score, commentaires).
- `olist_orders_dataset.csv`: Informations principales sur les commandes (ID de client, statut de la commande, timestamps d'achat, d'approbation, de livraison).
- `olist_products_dataset.csv`: Informations sur les produits (catégorie, dimensions, poids).
- `olist_sellers_dataset.csv`: Informations sur les vendeurs.
- `product_category_name_translation.csv`: Traduction des noms de catégories de produits en anglais.

## Étapes de l'Analyse

Le projet suit une méthodologie d'analyse de données structurée, comprenant les étapes suivantes :

1.  **Chargement & Nettoyage des Données :**
    *   Importation de tous les fichiers CSV dans des DataFrames pandas.
    *   Inspection initiale des données (informations sur les colonnes, types de données, valeurs nulles).
    *   Vérification et suppression des doublons dans chaque DataFrame.
    *   Traitement des valeurs manquantes, en particulier dans les colonnes clés (par exemple, suppression des lignes avec des dates de livraison manquantes dans `olist_orders_dataset`).

2.  **Transformation des Données :**
    *   Conversion des colonnes de dates (chaînes de caractères) en objets datetime.
    *   Calcul de la durée de livraison pour chaque commande (`delivery_duration` et `delivery_duration_days`).
    *   Calcul de l'écart entre la date de livraison estimée et la date réelle (`estimated_vs_real`).
    *   Création d'une colonne binaire (`on_time_delivery`) indiquant si la livraison a été effectuée à temps (oui/non).
    *   Agrégation des paiements par commande pour obtenir le montant total payé (`total_paid_per_order`).
    *   Calcul des frais de port moyens par commande.
    *   Agrégation des scores d'avis par commande (en prenant la moyenne si plusieurs avis existent pour une même commande).

3.  **Fusion et Enrichissement :**
    *   Sélection des colonnes pertinentes de chaque DataFrame.
    *   Fusion des DataFrames transformés (`orders_selected`, `total_paid_per_order`, `review_score`) en un DataFrame final (`final_df`) basé sur l'`order_id`.
    *   Ajout des informations de code postal du client (`customer_zip_code_prefix`) au `final_df`.
    *   Ajout des informations de ville du client (`geolocation_city`) au `final_df` en fusionnant avec les données de géolocalisation.

4.  **Analyse Exploratoire :**
    *   Analyse de la répartition des scores de satisfaction client (histogramme).
    *   Examen de l'impact du délai de livraison sur la satisfaction client (boxplot).
    *   Calcul du montant moyen des commandes en fonction du score de satisfaction.
    *   Identification des 5 villes avec le plus grand nombre de commandes livrées en retard.
    *   Identification des catégories de produits générant le plus de retards de livraison.
    *   Calcul du nombre moyen de jours de retard par catégorie de produit.

## Principaux Résultats/Visualisations

Quelques-unes des visualisations et analyses clés incluent :

*   **Répartition des scores de satisfaction :** Un histogramme montrant la distribution des notes données par les clients (1 à 5).
*   **Impact du délai de livraison sur la satisfaction :** Un boxplot comparant la durée de livraison en jours pour chaque score de satisfaction, afin d'identifier une éventuelle corrélation.
*   **Villes avec le plus de retards :** Un graphique à barres présentant les 5 villes ayant le plus grand nombre de commandes arrivées en retard.
*   **Catégories de produits et retards :** Des analyses pour déterminer quelles catégories de produits sont les plus sujettes aux retards de livraison et la durée moyenne de ces retards.

## Comment Exécuter le Notebook

Pour exécuter ce notebook Jupyter (`Project_Data_Analyst_Carlyna_Npower.ipynb`) et reproduire l'analyse, vous aurez besoin des bibliothèques Python suivantes :

*   pandas
*   numpy
*   matplotlib
*   seaborn

Vous pouvez les installer via pip si nécessaire :
```bash
pip install pandas numpy matplotlib seaborn
```

Assurez-vous également que les fichiers de données CSV  sont présents dans un sous-dossier nommé `Data/` par rapport à l'emplacement du notebook, ou modifiez les chemins de chargement des fichiers dans le notebook en conséquence.

Une fois l'environnement configuré, vous pouvez ouvrir et exécuter le notebook en utilisant Jupyter Notebook ou JupyterLab.

# Lab 1 — Du notebook au mini-système production-ready (MLOps)
**Préparé par :** ENIHE Nouhaila
## Étapes du lab

### Étape 1 — Initialiser la structure du projet
Mise en place d’une structure claire et standard pour un pipeline MLOps.  
La séparation des dossiers (**data, models, registry, logs, src**) permet d’isoler le code, les données, les modèles et les métadonnées, et facilite la traçabilité et la maintenance.

<img width="568" height="372" alt="Etape 1" src="https://github.com/user-attachments/assets/a1aff27b-f5ac-4013-8c3e-56a1438848a7" />


### Étape 2 — Préparer l’environnement Python
Création d’un **environnement virtuel Python** pour isoler les dépendances.  
Objectifs :
- exécuter le projet dans un environnement contrôlé et reproductible,
- éviter les conflits de versions,
- installer les bibliothèques nécessaires au pipeline (data, ML, API).

<img width="800" height="632" alt="Etape 2" src="https://github.com/user-attachments/assets/adbd663f-dfbd-43a9-91f5-c0cf23714c8c" />


### Étape 3 — Générer le dataset
Génération d’un **dataset synthétique** afin de disposer de données :
- cohérentes,
- reproductibles,
- indépendantes de données réelles.

Cette étape permet de tester tout le pipeline sans dépendance externe.

<img width="801" height="256" alt="Etape 3" src="https://github.com/user-attachments/assets/8618c88d-49a9-4a49-8569-253d9598161d" />


### Étape 4 — Préparer les données + quality checks
Nettoyage et préparation du dataset pour assurer la qualité avant entraînement :
- correction de valeurs aberrantes,
- normalisation / harmonisation des champs catégoriels,
- contrôles de cohérence (valeurs manquantes, types, bornes…).

Les données préparées sont sauvegardées séparément des données brutes, ce qui sécurise le pipeline et évite la propagation d’erreurs vers le modèle.

<img width="799" height="131" alt="Etape 4 1" src="https://github.com/user-attachments/assets/b8b6d0d0-1b88-46f4-9e61-ad5d55203fd4" />
<img width="799" height="608" alt="Etape 4 2" src="https://github.com/user-attachments/assets/1ee87ac1-54b7-4136-b63f-155e6013c5fe" />



### Étape 5 — Entraîner, versionner et valider le modèle
Entraînement d’un **modèle de régression logistique** à partir des données préparées via un pipeline scikit-learn intégrant :
- prétraitement,
- classification.

Évaluation avec des métriques standards :
- accuracy,
- precision,
- recall,
- F1,
et comparaison à une baseline simple.

Le modèle et ses métadonnées sont enregistrés dans une **registry** afin d’assurer la traçabilité (version, métriques, date, paramètres…).

<img width="804" height="549" alt="Etape 5 1" src="https://github.com/user-attachments/assets/ff8bb3e8-5db8-4bd3-b9bb-dbb25ce1e33e" />
<img width="799" height="639" alt="Etape 5 2" src="https://github.com/user-attachments/assets/9cd9cd48-a951-42b2-bb46-e924c7c93d43" />

### Étape 6 — Inspecter la registry et le modèle courant
Inspection des modèles disponibles dans la registry et identification du **modèle actif**.  
Cette étape illustre :
- la gestion des versions,
- la séparation entraînement/production,
- la garantie que seul un modèle validé est utilisé en production.

<img width="801" height="636" alt="Etape 6 1" src="https://github.com/user-attachments/assets/2aacbda9-cdc4-4f51-83dd-828be998578e" />
<img width="1422" height="790" alt="Etape 6 2" src="https://github.com/user-attachments/assets/11b4778f-64d7-498c-a142-b0ce971c8524" />


### Étape 7 — Créer une API `/predict` qui utilise le modèle courant
Exposition du modèle validé sous forme de service (API).  
Endpoints principaux :
- **`/predict`** : prédire le churn en temps réel à partir des features,
- **`/health`** : vérifier l’état du service et la disponibilité du modèle.

Cette étape montre comment intégrer un modèle ML dans une application réelle.

<img width="799" height="243" alt="Etape 7 1" src="https://github.com/user-attachments/assets/4017e3d9-8f83-4c45-af37-1352acc30e9a" />
<img width="1469" height="249" alt="Etape 7 2" src="https://github.com/user-attachments/assets/ef739d15-b9c5-466d-83fb-7183cf781edc" />
<img width="1470" height="879" alt="Etape 7 3" src="https://github.com/user-attachments/assets/a38bd70e-5e10-4dc5-afef-d57d01c7ed9e" />
<img width="1470" height="884" alt="Etape 7 4" src="https://github.com/user-attachments/assets/9f171e07-4f7a-4ab0-af94-367842a8af7a" />
<img width="1443" height="840" alt="Etape 7 5" src="https://github.com/user-attachments/assets/d7f87746-7069-4d01-820b-d0defb26e499" />
<img width="1444" height="831" alt="Etape 7 6" src="https://github.com/user-attachments/assets/9e48f75a-0921-4a56-bb15-1b0278abecfb" />
<img width="1424" height="836" alt="Etape 7 7" src="https://github.com/user-attachments/assets/bfcc578c-e55e-4ffd-b7b3-9c24da636148" />
<img width="1439" height="820" alt="Etape 7 8" src="https://github.com/user-attachments/assets/4a359ca2-90f8-4c74-b35f-2e1b6666a9c8" />


### Étape 8 — Détecter une dérive des données via les logs
Chaque requête est journalisée (logs) avec :
- données d’entrée,
- prédiction,
- version du modèle utilisée,
- timestamp.

Cela permet la traçabilité des décisions du modèle et la base du monitoring en production.

<img width="1428" height="821" alt="Etape 8 1" src="https://github.com/user-attachments/assets/a696e213-33e6-466c-8c36-ab62d21af8da" />
<img width="803" height="148" alt="Etape 8 2" src="https://github.com/user-attachments/assets/38d22933-21a1-420d-b4d4-7bf78e171c7d" />
<img width="803" height="135" alt="Etape 8 3" src="https://github.com/user-attachments/assets/3871f170-d826-41ca-b461-988015452ffe" />


### Étape 9 — Gérer les versions du modèle et revenir en arrière (rollback)
Mise en place d’un mécanisme de **détection du data drift** en comparant les statistiques :
- des données de production,
- avec celles du jeu d’entraînement.


<img width="803" height="566" alt="Etape 9 1" src="https://github.com/user-attachments/assets/6be6cdd4-7de9-4d18-9d5e-ea5838293bae" />
<img width="801" height="104" alt="Etape 9 2" src="https://github.com/user-attachments/assets/0f95c0ef-2831-4972-afa3-97d583855d60" />
<img width="1424" height="810" alt="Etape 9 3" src="https://github.com/user-attachments/assets/5f82bff4-4110-443b-8c7e-ca024b833ccf" />


# Lab 7 : Gestion du cycle de vie des modèles avec MLflow

## Points retenus

- Centralisation du suivi des expérimentations avec MLflow  
- Traçabilité complète des paramètres, métriques et artefacts  
- Gestion explicite des versions de modèles via le Model Registry  
- Séparation entre entraînement, activation et mise en production  
- Promotion et rollback de modèles sans modification du code applicatif  
- Chargement dynamique du modèle actif par l’API via un alias MLflow  


### Étape 1 : Initialisation de l’environnement et installation de MLflow
Création d’un environnement Python isolé (Python 3.12) et installation de la bibliothèque MLflow afin de garantir un environnement reproductible dédié au suivi des expériences et à la gestion des modèles.

<img width="646" height="844" alt="etape 1" src="https://github.com/user-attachments/assets/d7dc8561-4f09-46fc-b366-e8a806a408b5" />


### Étape 2 : Création explicite de l’espace de stockage MLflow
Mise en place d’une structure de stockage dédiée aux artefacts MLflow, permettant de séparer clairement les métadonnées (base de données) des fichiers générés par les entraînements (modèles, artefacts).

<img width="653" height="93" alt="etape 2" src="https://github.com/user-attachments/assets/ff088d7c-20b4-4610-a154-8404c8a399e5" />


### Étape 3 : Configuration du client MLflow
Configuration de l’URI du tracking server MLflow afin que tous les scripts d’entraînement envoient automatiquement leurs runs vers un serveur central plutôt que de les stocker localement.

<img width="853" height="81" alt="etape 3" src="https://github.com/user-attachments/assets/c25d6eb2-bca3-408c-a3bb-dce6d440d1b9" />


### Étape 4 : Démarrage du serveur MLflow (Tracking Server)
Lancement d’un serveur MLflow local utilisant SQLite comme backend et un artifact store dédié, faisant de MLflow la source centrale de vérité pour le suivi des expérimentations et des modèles.

<img width="848" height="776" alt="etape 4 1" src="https://github.com/user-attachments/assets/fde18805-a94a-411a-b152-3e89021a8e3c" />
<img width="1470" height="813" alt="etape 4 2" src="https://github.com/user-attachments/assets/a4cd3555-62a7-4d05-a19e-c8944a9c0f1a" />


### Étape 5 : Instrumentation de l’entraînement avec MLflow
Modification du script d’entraînement pour enregistrer automatiquement les paramètres, métriques, artefacts du modèle et publier chaque exécution comme une nouvelle version dans le Model Registry MLflow.

<img width="1108" height="778" alt="etape 5 1" src="https://github.com/user-attachments/assets/4c11a7bf-6c4f-46dd-a6eb-65e2c610011f" />
<img width="707" height="778" alt="etape 5 2" src="https://github.com/user-attachments/assets/bdc25c41-26ed-420b-8949-a10cb20a8151" />
<img width="712" height="130" alt="etape 5 2 2" src="https://github.com/user-attachments/assets/e81a77d5-be38-4592-92cb-beba431b06f4" />
<img width="1470" height="768" alt="etape 5 3" src="https://github.com/user-attachments/assets/f30e093d-5c83-40fb-b434-2bf6d7e46e0c" />
<img width="1470" height="705" alt="etape 5 4" src="https://github.com/user-attachments/assets/fe22f9d9-1d3a-464a-8ad5-c11e9242bbd3" />
<img width="1467" height="325" alt="etape 5 5" src="https://github.com/user-attachments/assets/f1548903-3c3a-49ef-8726-05c958b0662a" />


### Étape 6 : Observation du Model Registry MLflow
Analyse des modèles enregistrés via l’interface MLflow afin de visualiser les différentes versions, leurs métriques associées et leurs liens avec les runs d’entraînement.

<img width="1469" height="810" alt="etape 6 1" src="https://github.com/user-attachments/assets/788dbc3e-53d5-47cd-a2a7-610991b67050" />
<img width="1470" height="814" alt="etape 6 2" src="https://github.com/user-attachments/assets/14d2eced-657b-4807-9c7c-e565c7dc446b" />


### Étape 7 : Promotion explicite d’un modèle (Activation)
Implémentation d’un script de promotion permettant d’associer explicitement une version du modèle à l’alias `production`, rendant l’activation indépendante de l’entraînement.

<img width="709" height="415" alt="etape 7 1" src="https://github.com/user-attachments/assets/f8558210-d5a1-4c02-87cd-80e86aabe62a" />
<img width="1470" height="814" alt="etape 7 2" src="https://github.com/user-attachments/assets/61c4d671-588f-4acb-89b4-6d1b5e50f0b7" />


### Étape 8 : Rollback de modèle via le Model Registry MLflow
Mise en place d’un mécanisme de rollback permettant de revenir à une version précédente du modèle en modifiant uniquement l’alias `production`, sans modification du code ni des fichiers locaux.

<img width="1257" height="809" alt="etape 8 1" src="https://github.com/user-attachments/assets/1d737e62-9328-4a32-892a-30eab3ef31e4" />
<img width="707" height="142" alt="etape 8 2" src="https://github.com/user-attachments/assets/23fa167b-ec3c-45f8-901c-4b731778e6d4" />
<img width="1467" height="815" alt="etape 8 3" src="https://github.com/user-attachments/assets/8e3dd3dd-bab2-48f0-9a57-26a5b5a67a22" />


### Étape 9 : Chargement dynamique du modèle actif dans l’API
Adaptation de l’API FastAPI afin qu’elle charge dynamiquement le modèle actif depuis le Model Registry MLflow via l’alias `production`, garantissant la cohérence entre la version servie et la version validée.

<img width="768" height="326" alt="etape 9 1" src="https://github.com/user-attachments/assets/79b609ad-5e38-4a61-b45d-2e9aca551af1" />
<img width="781" height="257" alt="etape 9 2" src="https://github.com/user-attachments/assets/534e3e82-f26f-4145-9ccd-f58fb2eb5c47" />


## Résultat final

- Historique complet et traçable des entraînements  
- Gestion robuste des versions de modèles  
- Activation et rollback contrôlés et réversibles  
- API toujours alignée sur le modèle actif en production  

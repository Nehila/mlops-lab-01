## Lab3 : Versionnement des données et pipelines ML avec DVC

### Objectif
Versionner les données et les pipelines Machine Learning de manière reproductible,
sans surcharger Git.

### Points clés retenus
- Suivi des datasets via DVC (hash de contenu)
- Séparation entre code (Git) et données (DVC)
- Définition d’un pipeline de préparation, entraînement et évaluation
- Reproductibilité complète des expériences
- Traçabilité des versions de données et de modèles

## Étape 1 : Initialisation de DVC dans le projet
<img width="608" height="274" alt="etape 1" src="https://github.com/user-attachments/assets/e9416d16-dd35-41ec-a20b-916bbe9cf292" />

## Étape 2 : Versionner les données brutes avec DVC
Retrait de data/ du .gitignore pour activer le suivi DVC des données brutes.
<img width="722" height="183" alt="etape 2 1 " src="https://github.com/user-attachments/assets/d03e89e3-e032-4643-82f0-0c48887cc24b" />

Ajout du dataset au suivi DVC

<img width="625" height="300" alt="etape 2 2" src="https://github.com/user-attachments/assets/3ce3564a-387d-4683-bb4c-b2c9bdac5c25" />

## Étape 3 : Configuration d’un remote DVC
Configuration d’un remote DVC afin de centraliser le stockage des données et artefacts versionnés en dehors de Git.

<img width="624" height="74" alt="etape 3 1" src="https://github.com/user-attachments/assets/c26f110c-faaa-4501-9f5e-e793505a5588" />
<img width="621" height="111" alt="etape 3 2" src="https://github.com/user-attachments/assets/a41d7776-706e-4736-88a8-964b56fc1c00" />

## Étape 4 : Push des données dans le remote DVC
Envoi des données : 

<img width="626" height="76" alt="etape 4" src="https://github.com/user-attachments/assets/c1fc7471-54e2-4bf6-959a-7a3e55f74180" />

## Étape 5 : imulation d’une collaboration : supprimer localement et récupérer depuis DVC
Simulation d’un scénario collaboratif montrant que les données peuvent être supprimées localement et restaurées à l’identique depuis le remote DVC.

<img width="623" height="207" alt="etape 5" src="https://github.com/user-attachments/assets/300c93fc-7e43-43b5-8c9f-8ddddc038d48" />

## Étape 6 : Création d’un pipeline reproductible dvc.yaml
Structuration du pipeline d’entraînement et d’évaluation avec DVC afin de garantir la reproductibilité, le suivi des dépendances et la traçabilité des sorties.

<img width="623" height="748" alt="etape 6" src="https://github.com/user-attachments/assets/a596730d-a7e5-487a-a916-116d4331e06f" />

## Étape 7 : Reproduire automatiquement tout le pipeline
Traçabilité complète de l’exécution du pipeline ML à l’aide du fichier dvc.lock.

<img width="624" height="486" alt="etape 7 1" src="https://github.com/user-attachments/assets/448ebd05-43bc-4d35-a4f2-1248f46bdb13" />
<img width="624" height="445" alt="etape 7 2" src="https://github.com/user-attachments/assets/d36cc738-86f4-49f2-a947-adb6a437b408" />
<img width="622" height="90" alt="etape 7 3" src="https://github.com/user-attachments/assets/bfc98363-259c-401c-8e1e-8e8482cab148" />

### Résultat
Un pipeline ML reproductible et traçable, indépendant de la machine locale.

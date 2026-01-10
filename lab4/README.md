## Lab 4 : Mise en place d’un pipeline CI/CD complet pour un projet Machine Learning

### Objectif
Automatiser la validation du code, des données et du modèle à chaque évolution du projet.

### Points retenus
- Introduction à la CI/CD appliquée au Machine Learning
- Validation automatique du code et des dépendances
- Exécution contrôlée du pipeline ML
- Compréhension du rôle des runners et des workflows déclaratifs

## Étape 1 : Créer le dépôt GitHub et connecter le remote
Établir le lien entre le dépôt local et GitHub afin de centraliser le code et permettre l’automatisation des workflows CI/CD.

<img width="628" height="201" alt="etape 1" src="https://github.com/user-attachments/assets/a9f1428c-f96d-4d01-bf8d-c60553fcd61e" />

## Étape 2 : Définir les secrets GitHub
Définir des variables et des secrets sécurisés pour paramétrer le pipeline CI/CD sans exposer d’informations sensibles dans le dépôt.

<img width="795" height="145" alt="etape 2 1" src="https://github.com/user-attachments/assets/58db8f0a-1722-4b7f-a4d6-dfacd8fca162" />
<img width="796" height="238" alt="etape 2 2" src="https://github.com/user-attachments/assets/1a195511-d1f0-42f2-9d71-b65607b8daa6" />

## Étape 3 : Créer le workflow CI/CD
Décrire de manière déclarative les étapes d’intégration continue permettant de valider le code, les données et le modèle automatiquement.

<img width="550" height="18" alt="etape 3 1" src="https://github.com/user-attachments/assets/6c6b7202-33ab-4035-b277-00c7c5b4d98d" />
<img width="1470" height="848" alt="etape 3 2" src="https://github.com/user-attachments/assets/14dd4459-f15e-4e0a-b833-aa23c2a4e620" />
<img width="624" height="299" alt="etape 3 3" src="https://github.com/user-attachments/assets/1494047e-6829-4f40-9088-96881ce84262" />

## Étape 4 : Commit et push
Déclencher automatiquement l’exécution du pipeline CI/CD à chaque modification afin de détecter les régressions techniques et statistiques.


<img width="1456" height="651" alt="etape 4" src="https://github.com/user-attachments/assets/0bb3303f-9694-4052-976a-b3a7b2edd345" />






### Résultat
Un pipeline CI/CD capable de détecter les régressions techniques et statistiques.

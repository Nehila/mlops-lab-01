## Lab 5 : Du Notebook au Déploiement Conteneurisé d’un Modèle de Machine Learning

### Points retenus
- Conteneurisation avec Docker
- Exposition des endpoints `/health` et `/predict`
- Préparation à l’orchestration (Docker Compose)

## Étape 1 : Vérifier l’installation de Docker
<img width="829" height="121" alt="etape 1" src="https://github.com/user-attachments/assets/8fee705a-cf75-4979-b2f7-101a1b21f848" />

## Étape 2 : Lancer un serveur Nginx dans un conteneur
Mettre en évidence qu’un service web peut être exécuté de manière isolée et reproductible dans un conteneur Docker.

<img width="829" height="50" alt="etape 2 1" src="https://github.com/user-attachments/assets/08383240-96fa-4879-99f8-8b47e3864806" />
<img width="889" height="458" alt="etape 2 2" src="https://github.com/user-attachments/assets/d9888b92-9d36-4235-804d-5751b7df26cc" />
<img width="825" height="164" alt="etape 2 3" src="https://github.com/user-attachments/assets/d4ec40f2-aa97-4bb5-877a-1bb7f81088e2" />

## Étape 3 : Ouvrir un shell Linux isolé dans un conteneur
Illustrer que Docker permet de disposer d’un environnement Linux indépendant du système hôte pour tester et exécuter des commandes en toute isolation.

<img width="825" height="818" alt="etape 3 1" src="https://github.com/user-attachments/assets/44cbd8df-907c-4b96-b81e-e81ac91fae68" />
<img width="828" height="161" alt="etape 3 2" src="https://github.com/user-attachments/assets/614313b1-128c-434e-9e70-3dda83e53bf2" />

## Étape 4 : Comprendre la structure d’une commande docker run
Comprendre comment les options de docker run définissent le comportement du conteneur (mode détaché, ports, nom, image).

<img width="825" height="150" alt="etape 4" src="https://github.com/user-attachments/assets/2a11ffee-a20e-4946-a211-0f607d6a8ce1" />


## Étape 5 : Conteneuriser l’API churn du projet mlops-lab-01
Préparer le projet pour qu’il puisse être exécuté dans un environnement standardisé et indépendant de la machine locale.

<img width="821" height="203" alt="etape 5" src="https://github.com/user-attachments/assets/ea886e9e-1d83-4dda-8bac-ad7e0d08a580" />
<img width="822" height="149" alt="etape 5 2" src="https://github.com/user-attachments/assets/8042f5dc-3bd9-4e6c-bd12-3e9d30cb1bfe" />

## Étape 6 : Créer un fichier requirements.txt pour l’image Docker
Centraliser et figer les dépendances Python afin de garantir une installation identique dans tous les environnements.

<img width="827" height="140" alt="etape 6" src="https://github.com/user-attachments/assets/eff0a539-9429-432e-b81a-0fa405a28a09" />

## Étape 7 : Créer un Dockerfile pour l’API churn
Décrire de manière déclarative l’environnement d’exécution complet de l’API afin de produire une image Docker reproductible.

<img width="829" height="288" alt="etape 7" src="https://github.com/user-attachments/assets/14f0ec7a-6caa-4999-a0b3-5e39e4ef7a99" />

## Étape 8 :Préparer un modèle actif avant de construire l’image
S’assurer qu’un modèle validé et référencé est disponible avant l’intégration dans l’image Docker.

<img width="830" height="123" alt="etape 8" src="https://github.com/user-attachments/assets/751a0de8-e18e-44ea-a392-d7ba1fafc4e0" />

## Étape 9 : Construire l’image Docker du projet churn
Transformer le code, les dépendances et la configuration en un artefact unique exécutable sur n’importe quelle machine.

<img width="826" height="546" alt="etape 9" src="https://github.com/user-attachments/assets/430d5108-e5e3-4af3-bfd9-b9f1e63bc1d2" />

## Étape 10 : Lancer l’API churn dans un conteneur
Valider que l’API fonctionne correctement lorsqu’elle est exécutée à partir de l’image Docker construite.

<img width="824" height="162" alt="etape 10 1" src="https://github.com/user-attachments/assets/5edeb901-d51b-4a1c-828f-5189e3bd9437" />
<img width="565" height="284" alt="etape 10 2" src="https://github.com/user-attachments/assets/77227e09-6403-4a5b-bb21-43d66564075d" />

## Étape 11 : Vérifier les logs générés à l’intérieur du conteneur
Observer les prédictions et les métadonnées pour assurer la traçabilité et le monitoring du service d’inférence.

<img width="829" height="331" alt="etape 11" src="https://github.com/user-attachments/assets/abad39f2-36d4-49b5-920a-50919b8e4fb9" />

## Étape 12 : Orchestration locale avec Docker Compose
Décrire et lancer plusieurs services de manière cohérente à l’aide d’un fichier déclaratif unique.

<img width="829" height="249" alt="etape 12" src="https://github.com/user-attachments/assets/97bfa690-29da-40d3-b0f2-5374b8c0bc5c" />

## Étape 13 : Démarrer l’API via Docker Compose
Démontrer que l’ensemble du service peut être lancé et arrêté de façon reproductible avec une seule commande.

<img width="827" height="334" alt="etape 13" src="https://github.com/user-attachments/assets/c82bfde1-9313-4754-bbce-2496471c79e1" />

## Étape 14 : lancer les services en arrière-plan et observer les logs
Exécuter les services en mode détaché tout en conservant la capacité de supervision via les logs.

<img width="826" height="596" alt="etape 14" src="https://github.com/user-attachments/assets/cf3b8876-8289-4228-9859-c6b73df2e08f" />

## Étape 15 : lier Docker Compose au reste du cours (Git + DVC)

<img width="1446" height="689" alt="Screenshot 2026-01-10 at 17 15 06" src="https://github.com/user-attachments/assets/5bc7318f-ff66-4685-82f1-8b471e48980a" />


### Résultat
Un service d’inférence prêt à être exécuté de manière identique sur tout environnement.

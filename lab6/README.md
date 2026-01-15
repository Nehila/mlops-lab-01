# Lab 6 : Déploiement d’une API Churn sur Kubernetes

## Points retenus

- Conteneurisation de l’API de prédiction churn à l’aide de Docker avec versionnement explicite des images  
- Déploiement de l’API sur un cluster Kubernetes local via Minikube  
- Isolation des ressources grâce à un namespace Kubernetes dédié  
- Gestion sécurisée des informations sensibles à l’aide de Secrets Kubernetes  
- Mise en place de volumes persistants pour la conservation des modèles et des logs  
- Supervision automatique de l’API à l’aide des probes Kubernetes (liveness, readiness, startup)  
- Sécurisation des flux réseau grâce aux NetworkPolicy  
- Validation du pipeline MLOps par des tests fonctionnels et des scripts de monitoring (détection de drift)

## Étapes 

### Étape 1 : Préparation de l’environnement Kubernetes
Initialisation d’un cluster Kubernetes local avec Minikube (driver Docker), création d’un namespace dédié (`churn-mlops`) et configuration du contexte courant afin d’isoler les ressources du laboratoire MLOps.

<img width="586" height="694" alt="etape 1" src="https://github.com/user-attachments/assets/a642132e-fbab-49e6-8c11-48fb311be664" />


### Étape 2 : Préparation de l’image Docker de l’API churn
Mise en place d’un environnement Python strictement versionné (Python 3.12), définition explicite des dépendances dans `requirements.txt` et installation contrôlée des librairies pour garantir la compatibilité entre l’entraînement du modèle et l’inférence via l’API.

<img width="606" height="211" alt="etape 2 1" src="https://github.com/user-attachments/assets/3672650f-c6e2-4f40-b51c-13cf91c34b13" />
<img width="599" height="774" alt="etape 2 2" src="https://github.com/user-attachments/assets/b791b3eb-f83f-47e9-9a82-efc02440b4b2" />


### Étape 3 : Création du dossier des manifests Kubernetes
Création d’un dossier `k8s/` destiné à centraliser tous les manifests Kubernetes (Deployment, Service, ConfigMap, Secret, etc.), facilitant la maintenabilité et la reproductibilité du déploiement.

<img width="605" height="706" alt="etape 3" src="https://github.com/user-attachments/assets/a60aa0e7-d31c-4ba0-b6c6-d85c927ce5e1" />


### Étape 4 : Construction de l’image Docker avec tag versionné
Construction de l’image Docker de l’API churn avec un tag de version explicite (`v1`), garantissant la traçabilité des versions et évitant l’utilisation du tag `latest`.

<img width="798" height="428" alt="etape 4" src="https://github.com/user-attachments/assets/beec06b3-1c03-4b33-a7e9-c6287beddc27" />



### Étape 5 : Chargement explicite de l’image Docker dans Minikube
Export de l’image Docker et chargement manuel dans Minikube afin de rendre l’image disponible au cluster local sans dépendre d’un registry externe.

<img width="797" height="115" alt="etape 5" src="https://github.com/user-attachments/assets/73cdf227-ed8c-445c-a214-ad6b4d038ef4" />


### Étape 6 : Déploiement Kubernetes de l’API churn
Déploiement de l’API sous forme de Deployment Kubernetes avec plusieurs réplicas, suivi du rollout et vérification que les Pods sont opérationnels dans le namespace `churn-mlops`.

<img width="803" height="270" alt="etape 6" src="https://github.com/user-attachments/assets/2385c1a8-67e1-4251-ada6-7f84a3c47e64" />


### Étape 7 : Exposition de l’API via un Service NodePort
Création d’un Service Kubernetes de type NodePort permettant l’accès externe à l’API churn et le test des endpoints de prédiction depuis l’extérieur du cluster.

<img width="801" height="564" alt="etape 7 1" src="https://github.com/user-attachments/assets/c778fd82-0798-4253-a15f-c25ff8eae4db" />
<img width="782" height="764" alt="etape 7 2" src="https://github.com/user-attachments/assets/56dda82a-2d3c-41d0-82d0-de94e7ae0e38" />
<img width="800" height="161" alt="etape 7 2 1" src="https://github.com/user-attachments/assets/b3884f47-f1e6-470a-950a-375b5468036c" />
<img width="783" height="510" alt="etape 7 3" src="https://github.com/user-attachments/assets/b245ceab-8aeb-418a-a6ec-872caff4ec91" />
<img width="758" height="752" alt="etape 7 4" src="https://github.com/user-attachments/assets/3f0d6d89-84cc-486b-8a74-723440a77db1" />


### Étape 8 : Injection de la configuration MLOps via ConfigMap
Externalisation des paramètres applicatifs (nom du modèle, niveau de logs, etc.) dans un ConfigMap et injection dynamique de ces variables dans les Pods, séparant clairement configuration et code.

<img width="809" height="539" alt="etape 8 1" src="https://github.com/user-attachments/assets/a4fec538-091e-462f-82e1-ef54eb9ce8ce" />
<img width="667" height="648" alt="etape 8 2" src="https://github.com/user-attachments/assets/013272e3-8fd6-4c32-8cdd-288e26ba9a40" />
<img width="813" height="263" alt="etape 8 3" src="https://github.com/user-attachments/assets/57c1395e-0b2e-49d7-a18c-0b8431c81ff4" />




### Étape 9 : Gestion sécurisée des secrets (MONITORING_TOKEN)
Stockage et injection sécurisée des informations sensibles via un Secret Kubernetes, garantissant la confidentialité des tokens de monitoring.

<img width="811" height="456" alt="etape 9 1" src="https://github.com/user-attachments/assets/0f7396aa-2028-4eb9-a7d4-0ae523290c15" />
<img width="609" height="350" alt="etape 9 2" src="https://github.com/user-attachments/assets/08b6b6ca-8ee3-403b-920f-2ff74994a544" />
<img width="808" height="187" alt="etape 9 3" src="https://github.com/user-attachments/assets/16b20602-519d-48d1-bef2-a8e3fbd104f9" />



### Étape 10 : Mise en place des endpoints de santé de l’API churn
Ajout des endpoints `/health`, `/ready` et `/startup` dans l’API FastAPI afin de permettre à Kubernetes d’évaluer l’état de santé, la disponibilité et le bon démarrage de l’application.

<img width="990" height="795" alt="etape 10 1" src="https://github.com/user-attachments/assets/47f1b5ef-44ee-4ad6-8eff-f97a651313ea" />
<img width="808" height="443" alt="etape 10 2" src="https://github.com/user-attachments/assets/853b9595-8a78-4f2c-a869-56283b50f85a" />


### Étape 11 : Configuration des probes Kubernetes
Mise en place des probes de liveness, readiness et startup pour automatiser la supervision, redémarrer les Pods défaillants et router le trafic uniquement vers les Pods prêts.

<img width="558" height="456" alt="etape 11 1" src="https://github.com/user-attachments/assets/45cff16e-0498-40e1-92e6-026cd14f5326" />
<img width="802" height="828" alt="etape 11 2" src="https://github.com/user-attachments/assets/c0055a7d-b88f-4956-af81-c5fc77e1b856" />
<img width="1033" height="248" alt="etape 11 5" src="https://github.com/user-attachments/assets/8fca7ec0-9c1d-4bb9-97d5-33e93d9dc02d" />


### Étape 12 : Mise en place d’un volume persistant pour les modèles et logs
Création d’un PersistentVolumeClaim (PVC) pour stocker durablement les modèles, le registry et les logs, puis exécution d’un Job Kubernetes d’entraînement initial afin d’initialiser le stockage partagé.

<img width="846" height="282" alt="etape 12 1" src="https://github.com/user-attachments/assets/f18b5a24-6f24-45a4-a539-9b4a09fffce0" />
<img width="597" height="221" alt="etape 12 2" src="https://github.com/user-attachments/assets/af8e22ea-eca8-4ac0-b835-f672633d1c45" />
<img width="852" height="683" alt="etape 12 3" src="https://github.com/user-attachments/assets/38637648-0710-4323-aa12-1a01b8f799c2" />
<img width="680" height="568" alt="etape 12 4" src="https://github.com/user-attachments/assets/7db36157-bd91-4f52-ae73-d1c0b6ec4900" />


### Étape 13 : Sécurisation réseau via NetworkPolicy
Application d’une NetworkPolicy afin de restreindre les flux réseau et autoriser uniquement les communications nécessaires vers l’API churn, renforçant la sécurité du déploiement.

<img width="848" height="386" alt="etape 13" src="https://github.com/user-attachments/assets/8a463d5a-d318-48f3-b63a-06a0bb6d27e1" />


### Étape 14 : Vérifications finales et validation du pipeline
Vérification globale du système : état des Pods et Services, tests des endpoints de santé et de prédiction, et exécution des scripts de monitoring (détection de drift) pour valider le pipeline MLOps de bout en bout.

<img width="828" height="281" alt="etape 14 1" src="https://github.com/user-attachments/assets/1a2512c7-1971-41d5-bcff-714fdf63c473" />
<img width="814" height="668" alt="etape 14 2" src="https://github.com/user-attachments/assets/774eea96-8f16-49d1-839f-c980a9f90cc8" />
<img width="817" height="755" alt="etape 14 3" src="https://github.com/user-attachments/assets/5713c09d-dbd3-4f59-9876-b5ef5a00324e" />
<img width="822" height="553" alt="etape 14 3 3" src="https://github.com/user-attachments/assets/9534c387-4387-46bf-a8b7-e0e4caf6cacd" />
<img width="850" height="76" alt="etape 14 4" src="https://github.com/user-attachments/assets/ecf41c4d-db90-4fb1-ab5a-37dc8586419d" />
<img width="849" height="171" alt="etape 14 5" src="https://github.com/user-attachments/assets/dfb2049c-2ca4-42da-8077-5e12adb7a556" />



## Résultat final

- API churn opérationnelle et scalable sur Kubernetes  
- Pipeline MLOps reproductible et sécurisé  
- Configuration, secrets et modèles correctement externalisés  
- Supervision automatique et tolérance aux pannes assurées  

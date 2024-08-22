# Déploiement d’une App Front & Back sur ECS

![](<Architecture App.png>)

## Coûts estimation :

## Fonctionnalités :
- Déploiement d’une application haute disponible et resiliente à deux niveaux: Couche presentation & metier et couche base de données: Cas de wordpress
- Auto scaling
- Load Balancing
- Persistance des données

## Services :

### Réseau
- **VPC (Virtual Private Cloud)** : Fournit un réseau isolé dans le cloud, permettant de définir des sous-réseaux, des règles de sécurité, et des connexions à Internet.
- **SUBNET (Sous-réseau)** : Divise un VPC en segments plus petits pour organiser les ressources et gérer la sécurité.
- **INTERNET GATEWAY** : Permet la communication entre les ressources dans un VPC et Internet.
- **EIP (Elastic IP)** : Adresse IP statique qui peut être associée à une instance pour la rendre accessible sur Internet.
- **ALB (Application Load Balancer)** : Distribue le trafic entrant entre plusieurs cibles (instances EC2, conteneurs, etc.) et permet de gérer le routage basé sur le contenu.
- **ACL (Access Control List)** : Définit des règles de sécurité pour contrôler le trafic entrant et sortant au niveau des sous-réseaux.
- **NAT (Network Address Translation)** : Permet aux instances dans un sous-réseau privé d'accéder à Internet sans exposer leurs adresses IP.
- **ROUTE (Table de routage)** : Définit les règles de routage pour diriger le trafic entre les sous-réseaux et vers Internet.
- **SECURITY GROUP** : Agit comme un pare-feu virtuel pour contrôler le trafic entrant et sortant des instances.

### Réseau et DNS
- **ROUTE 53** : Service DNS qui permet de gérer les noms de domaine et de diriger le trafic vers les ressources AWS.

### Sécurité
- **SECRET MANAGER** : Service qui permet de stocker et de gérer les secrets (comme les mots de passe et les clés API) de manière sécurisée.
- **IAM (Identity and Access Management)** : Définir ce que les utilisateurs et les rôles peuvent faire avec les ressources AWS.
  - **Rôle** : Un rôle IAM est une entité qui définit un ensemble de permissions pour effectuer des actions sur des ressources AWS. Contrairement aux utilisateurs, les rôles ne sont pas associés à une personne ou un compte spécifique, mais peuvent être assumés par des services AWS, des utilisateurs ou des applications. Les rôles sont souvent utilisés pour accorder des permissions temporaires.
  - **Permission** : Définir ce que les utilisateurs et les rôles peuvent faire avec les ressources AWS.
- **AWS Certificate Manager (ACM)**: permet de provisionner, gérer et déployer des certificats SSL/TLS publics et privés pour sécuriser les communications avec les services AWS et les ressources internes connectées12.
 
### Stockage
- **S3 (Simple Storage Service)** : Service de stockage d'objets pour stocker et récupérer des données à tout moment.
- **EFS (Elastic File System)** : Système de fichiers évolutif qui peut être monté sur plusieurs instances EC2.

### Base de données
- **RDS (Relational Database Service)** : Service de base de données relationnelle géré pour MySQL, PostgreSQL, Oracle, SQL Server et MariaDB.

### Calcul (Conteneurs)
- **ECS (Elastic Container Service)** : Service d’orchestration de conteneurs qui facilite le déploiement et la gestion d'applications conteneurisées.
- **Fargate** : est un service de calcul sans serveur qui permet de déployer et de gérer des conteneurs sans avoir à gérer l'infrastructure sous-jacente. Il fonctionne avec des services comme Amazon ECS (Elastic Container Service) et Amazon EKS (Elastic Kubernetes Service).
- **Task** : Unité de travail dans ECS qui définit un ensemble de conteneurs à exécuter ensemble.
- **Task Definition** : Modèle qui définit les paramètres pour les tâches ECS, y compris les images de conteneur, les ressources, et les configurations réseau.
- **Auto Scaling** : Surveille vos applications et ajuste automatiquement la capacité pour maintenir des performances constantes et prévisibles au coût le plus bas possible.


### Surveillance et Gestion des Ressources
- **CLOUDWATCH** : Service de surveillance qui collecte et suit les métriques, les journaux, et les événements pour les ressources AWS.
  - **Container Insight** : Outil de surveillance pour les conteneurs.
  - **Logs Groups** : Regroupe les journaux pour une gestion et une analyse centralisées.

  

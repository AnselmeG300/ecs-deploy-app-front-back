Voici une explication de chaque propriété de la définition de tâche AWS ECS:

### `containerDefinitions`
- **name**: Nom du conteneur, ici "wordpress-front".
- **image**: Image Docker utilisée, ici "bitnami/wordpress".
- **cpu**: Quantité de CPU allouée au conteneur. Ici, 0 signifie qu'il n'y a pas de réservation spécifique.
- **portMappings**: Mappage des ports entre le conteneur et l'hôte.
  - **containerPort**: Port utilisé dans le conteneur, ici 8080.
  - **hostPort**: Port utilisé sur l'hôte, ici 8080.
  - **protocol**: Protocole utilisé, ici TCP.
- **essential**: Indique si ce conteneur est essentiel pour la tâche. Si ce conteneur échoue, la tâche échoue également.
- **environment**: Variables d'environnement pour le conteneur.
  - **MARIADB_HOST**: Hôte de la base de données MariaDB.
  - **ECS_RESERVED_MEMORY**: Mémoire réservée pour ECS.
  - **PHP_MEMORY_LIMIT**: Limite de mémoire pour PHP.
  - **enabled**: Variable personnalisée, ici désactivée.
  - **WORDPRESS_DATABASE_NAME**: Nom de la base de données WordPress.
- **mountPoints**: Points de montage pour les volumes.
  - **sourceVolume**: Nom du volume source, ici "efs-wordpress-volume".
  - **containerPath**: Chemin dans le conteneur où le volume est monté, ici "/bitnami/wordpress".
- **volumesFrom**: Volumes hérités d'autres conteneurs (vide ici).
- **secrets**: Secrets gérés par AWS Secrets Manager.
  - **WORDPRESS_DATABASE_USER**: Utilisateur de la base de données WordPress.
  - **WORDPRESS_DATABASE_PASSWORD**: Mot de passe de la base de données WordPress.
- **user**: Utilisateur sous lequel le conteneur s'exécute, ici "root".
- **logConfiguration**: Configuration des logs.
  - **logDriver**: Pilote de logs utilisé, ici "awslogs".
  - **options**: Options pour la configuration des logs.
    - **awslogs-group**: Groupe de logs AWS.
    - **awslogs-create-group**: Indique si le groupe de logs doit être créé.
    - **awslogs-region**: Région AWS pour les logs.
    - **awslogs-stream-prefix**: Préfixe pour les flux de logs.
- **systemControls**: Contrôles système (vide ici).

### `family`
Nom de la famille de tâches, ici "wordpress-front".

### `executionRoleArn`
ARN du rôle d'exécution IAM utilisé par la tâche.

### `networkMode`
Mode réseau utilisé par la tâche, ici "awsvpc".

### `revision`
Numéro de révision de la définition de tâche, ici 2.

### `volumes`
Volumes utilisés par la tâche.
- **name**: Nom du volume, ici "efs-wordpress-volume".
- **efsVolumeConfiguration**: Configuration du volume EFS.
  - **fileSystemId**: ID du système de fichiers EFS.
  - **rootDirectory**: Répertoire racine du volume.
  - **transitEncryption**: Chiffrement en transit, ici activé.
  - **authorizationConfig**: Configuration de l'autorisation.
    - **accessPointId**: ID du point d'accès.
    - **iam**: Indique si IAM est utilisé pour l'autorisation, ici désactivé.

### `placementConstraints`
Contraintes de placement pour la tâche (vide ici).

### `compatibilities`
Compatibilités de la tâche, ici "EC2" et "FARGATE".

### `requiresCompatibilities`
Compatibilités requises pour la tâche, ici "FARGATE".

### `cpu`
Quantité de CPU allouée à la tâche, ici 1024 unités (1 vCPU).

### `memory`
Quantité de mémoire allouée à la tâche, ici 2048 Mo (2 Go).

### `registeredAt`
Date et heure d'enregistrement de la définition de tâche.

### `registeredBy`
ARN de l'utilisateur qui a enregistré la définition de tâche.

### `tags`
Étiquettes associées à la tâche.
- **key**: Clé de l'étiquette, ici "Name".
- **value**: Valeur de l'étiquette, ici "wordpress-prod-task-front".

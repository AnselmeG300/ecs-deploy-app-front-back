# Deployment of a Front & Back App on ECS

![](<Deploy Worspress ECS.png>)

## Cost Estimation:

## Features:
- Deployment of a front-end and back-end application
- Auto scaling
- Load balancing
- Data persistence

## Services:

### Networking
- **VPC (Virtual Private Cloud)**: Provides an isolated network in the cloud, allowing the definition of subnets, security rules, and Internet connections.
- **SUBNET**: Divides a VPC into smaller segments to organize resources and manage security.
- **INTERNET GATEWAY**: Enables communication between resources in a VPC and the Internet.
- **EIP (Elastic IP)**: A static IP address that can be associated with an instance to make it accessible on the Internet.
- **ALB (Application Load Balancer)**: Distributes incoming traffic among multiple targets (EC2 instances, containers, etc.) and allows content-based routing.
- **ACL (Access Control List)**: Defines security rules to control incoming and outgoing traffic at the subnet level.
- **NAT (Network Address Translation)**: Allows instances in a private subnet to access the Internet without exposing their IP addresses.
- **ROUTE (Route Table)**: Defines routing rules to direct traffic between subnets and to the Internet.
- **SECURITY GROUP**: Acts as a virtual firewall to control incoming and outgoing traffic for instances.

### Service Discovery and Management
- **CLOUDMAP**: A service discovery service that allows applications to find and connect to other services.
- **ROUTE 53**: A DNS service that manages domain names and directs traffic to AWS resources.

### Containers and Orchestration
- **ECS (Elastic Container Service)**: A container orchestration service that simplifies the deployment and management of containerized applications.
- **Task**: A unit of work in ECS that defines a set of containers to run together.
- **Task Definition**: A model that defines the parameters for ECS tasks, including container images, resources, and network configurations.

### Security
- **SECRET MANAGER**: A service that allows for the secure storage and management of secrets (such as passwords and API keys).
- **IAM (Identity and Access Management)**: Defines what users and roles can do with AWS resources.
  - **Role**: An IAM role is an entity that defines a set of permissions to perform actions on AWS resources. Unlike users, roles are not associated with a specific person or account but can be assumed by AWS services, users, or applications. Roles are often used to grant temporary permissions.
  - **Permission**: Defines what users and roles can do with AWS resources.

### Monitoring and Resource Management
- **CLOUDWATCH**: A monitoring service that collects and tracks metrics, logs, and events for AWS resources.
  - **Container Insight**: A monitoring tool for containers.
  - **Logs Groups**: Groups logs for centralized management and analysis.

### Storage
- **S3 (Simple Storage Service)**: An object storage service for storing and retrieving data at any time.
- **EBS (Elastic Block Store)**: Provides persistent block storage for EC2 instances.
- **EFS (Elastic File System)**: A scalable file system that can be mounted on multiple EC2 instances.
- **DLM (Data Lifecycle Manager)**: Automates the management of backups and snapshots for EBS volumes.

### Simplified Services
- **LIGHTSAIL**: A simplified service for deploying applications and websites using virtual instances.
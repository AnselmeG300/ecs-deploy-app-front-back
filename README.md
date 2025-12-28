
# ECS Deploy App - WordPress Front & Back

A production-ready WordPress deployment on AWS ECS (Elastic Container Service) using Docker containers, showcasing modern cloud infrastructure and containerization best practices.

## 🚀 Overview

This project demonstrates a scalable, highly available WordPress application deployed on AWS ECS Fargate. It leverages Docker containers for consistent deployment across environments, with a focus on security, performance, and automation.

## 🏗️ Architecture

The deployment architecture includes:

![](<Architecture App.png>)

- **Container Platform**: AWS ECS Fargate (serverless containers)
- **Application**: WordPress 6.5.5 with PHP 8.1 & Apache
- **Database**: Amazon RDS with RDS Proxy for connection pooling
- **Storage**: Amazon EFS (Elastic File System) for persistent WordPress data
- **Secrets Management**: AWS Secrets Manager for secure credential storage
- **Logging**: CloudWatch Logs for centralized log management
- **Networking**: VPC with proper security groups and private/public subnets

## 🐳 Docker Configuration

### WordPress Container

The application uses the official WordPress Docker image with specific optimizations:

- **Base Image**: `wordpress:6.5.5-php8.1-apache`
- **CPU**: 1024 units (1 vCPU)
- **Memory**: 2048 MB (2 GB)
- **PHP Memory Limit**: 512M for optimal performance
- **Port Mapping**: Container port 80 → Host port 80

### Container Features

- ✅ **Rootless capable** with configurable user permissions
- ✅ **EFS integration** for persistent WordPress files and media
- ✅ **CloudWatch logging** with automatic log group creation
- ✅ **Secrets injection** from AWS Secrets Manager
- ✅ **Health monitoring** and auto-restart capabilities

## 📦 Deployment

### Prerequisites

- AWS Account with appropriate permissions
- AWS CLI configured
- Docker installed (for local testing)
- ECS CLI (optional, for easier deployment)

### Task Definition

The project includes a production-ready ECS task definition (`tasks-definition/wordpress-front.json`) that defines:

```json
{
  "family": "wordpress-front-new",
  "requiresCompatibilities": ["FARGATE"],
  "networkMode": "awsvpc",
  "cpu": "1024",
  "memory": "2048"
}
```

### Deployment Steps

1. **Register the Task Definition**:
   ```bash
   aws ecs register-task-definition \
     --cli-input-json file://tasks-definition/wordpress-front.json
   ```

2. **Create or Update ECS Service**:
   ```bash
   aws ecs create-service \
     --cluster your-cluster-name \
     --service-name wordpress-front-service \
     --task-definition wordpress-front-new \
     --desired-count 2 \
     --launch-type FARGATE \
     --network-configuration "awsvpcConfiguration={subnets=[subnet-xxx],securityGroups=[sg-xxx],assignPublicIp=ENABLED}"
   ```

3. **Deploy with Load Balancer** (recommended):
   ```bash
   aws ecs create-service \
     --cluster your-cluster-name \
     --service-name wordpress-front-service \
     --task-definition wordpress-front-new \
     --desired-count 2 \
     --launch-type FARGATE \
     --network-configuration "awsvpcConfiguration={subnets=[subnet-xxx],securityGroups=[sg-xxx]}" \
     --load-balancers "targetGroupArn=arn:aws:elasticloadbalancing:.. .,containerName=wordpress-front,containerPort=80"
   ```

## 🔒 Security

### Secrets Management

Database credentials are securely stored in AWS Secrets Manager and injected at runtime:

- **WORDPRESS_DB_USER**: Retrieved from Secrets Manager
- **WORDPRESS_DB_PASSWORD**: Retrieved from Secrets Manager
- **No hardcoded credentials** in the codebase

### Network Security

- VPC isolation with private subnets for database
- RDS Proxy for secure database connections
- Security groups restricting traffic flow
- EFS encryption in transit enabled

### IAM Roles

- **Execution Role**: `wordpress-prod-role` with minimal required permissions
- Follows AWS principle of least privilege

## 📊 Infrastructure Components

| Component | Service | Purpose |
|-----------|---------|---------|
| Compute | ECS Fargate | Serverless container orchestration |
| Database | RDS (via Proxy) | Managed MySQL/MariaDB |
| Storage | EFS | Persistent file storage |
| Secrets | Secrets Manager | Credential management |
| Logging | CloudWatch Logs | Centralized logging |
| Networking | VPC + Subnets | Network isolation |

## 🔧 Configuration

### Environment Variables

- `WORDPRESS_DB_HOST`: RDS Proxy endpoint
- `WORDPRESS_DB_NAME`: Database name (wordpressdatabase)
- `PHP_MEMORY_LIMIT`: Set to 512M
- `ECS_RESERVED_MEMORY`: 100MB reserved for system

### Volume Mounts

```json
{
  "sourceVolume": "efs-wordpress-volume",
  "containerPath": "/bitnami/wordpress"
}
```

## 📈 Scaling

The Fargate deployment supports:

- **Horizontal Scaling**:  Increase task count for more capacity
- **Auto Scaling**: Configure based on CPU/Memory metrics
- **Load Balancing**:  Distribute traffic across multiple tasks

Example auto-scaling configuration: 
```bash
aws application-autoscaling register-scalable-target \
  --service-namespace ecs \
  --resource-id service/your-cluster/wordpress-front-service \
  --scalable-dimension ecs:service:DesiredCount \
  --min-capacity 2 \
  --max-capacity 10
```

## 🔍 Monitoring & Logging

### CloudWatch Logs

All container logs are automatically sent to CloudWatch: 

- **Log Group**: `wordpress-front-container`
- **Region**: `eu-west-1`
- **Stream Prefix**: `wordpress-front`

### Viewing Logs

```bash
aws logs tail wordpress-front-container --follow
```

## 🚦 CI/CD Integration

This setup is ready for CI/CD integration with:

- GitHub Actions
- AWS CodePipeline
- Jenkins
- GitLab CI

Example GitHub Actions workflow snippet:
```yaml
- name: Deploy to ECS
  run: |
    aws ecs update-service \
      --cluster your-cluster \
      --service wordpress-front-service \
      --force-new-deployment
```

## 🛠️ Local Development

Test the Docker container locally:

```bash
docker run -d \
  -p 8080:80 \
  -e WORDPRESS_DB_HOST=localhost \
  -e WORDPRESS_DB_NAME=wordpress \
  -e WORDPRESS_DB_USER=root \
  -e WORDPRESS_DB_PASSWORD=password \
  wordpress:6.5.5-php8.1-apache
```

## 📝 Task Definition Tags

- **Name**: `wordpress-prod-task-front`
- Easy identification in AWS Console
- Cost allocation tracking

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## 📄 License

This project is licensed under the MIT License.

## 🙋‍♂️ Support

For issues and questions:
- Open an issue in this repository
- Check AWS ECS documentation
- Review CloudWatch logs for troubleshooting

## 🔗 Useful Links

- [AWS ECS Documentation](https://docs.aws.amazon.com/ecs/)
- [Docker WordPress Image](https://hub.docker.com/_/wordpress)
- [AWS Fargate Pricing](https://aws.amazon.com/fargate/pricing/)
- [EFS Best Practices](https://docs.aws.amazon.com/efs/latest/ug/best-practices.html)

---

**Built with ❤️ using Docker and AWS ECS**

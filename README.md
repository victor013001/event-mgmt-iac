### Available Variables (Examples)

The `terraform.tfvars.example` file contains all possible variables you can configure with example values:

| Variable                                    | Description                              | Default                  | Required |
|---------------------------------------------|------------------------------------------|--------------------------|----------|
| `region`                                    | AWS region to deploy resources           | `us-east-1`              | No       |
| `app_name`                                  | Base name for application resources      | `event-mgmt`             | No       |
| `vpc_cidr`                                  | CIDR block for the VPC                   | `10.0.0.0/16`            | No       |
| `ecr_repository_name`                       | ECR repository name                      | `event-mgmt`             | No       |
| `ecr_image_tag`                             | ECR image tag to deploy                  | `latest`                 | No       |
| `active_profile`                            | Spring Boot profile                      | `dev`                    | No       |
| `ecs_cpu`                                   | ECS Fargate CPU units                    | `256`                    | No       |
| `ecs_memory`                                | ECS Fargate memory (MiB)                 | `512`                    | No       |
| `ecs_desired_count`                         | Number of ECS tasks                      | `1`                      | No       |
| `ecs_container_port`                        | Application port                         | `8080`                   | No       |
| `ecs_log_retention_days`                    | ECS log retention                        | `1`                      | No       |
| `apigw_log_retention_days`                  | API Gateway log retention                | `1`                      | No       |
| `aws_dynamodb_endpoint`                     | DynamoDB endpoint (for LocalStack)       | `""`                     | No       |
| `adapter_sqs_endpoint`                      | SQS adapter endpoint (for LocalStack)    | `""`                     | No       |
| `entrypoint_sqs_endpoint`                   | SQS entrypoint endpoint (for LocalStack) | `""`                     | No       |
| `entrypoint_sqs_wait_time_seconds`          | SQS wait time                            | `20`                     | No       |
| `entrypoint_sqs_max_number_of_messages`     | SQS max messages                         | `10`                     | No       |
| `entrypoint_sqs_visibility_timeout_seconds` | SQS visibility timeout                   | `30`                     | No       |
| `entrypoint_sqs_number_of_threads`          | SQS consumer threads                     | `1`                      | No       |
| `cors_allowed_origins`                      | CORS allowed origins                     | `https://localhost:3000` | No       |
| `scheduler_ticket_expiration_fixed_delay`   | Scheduler delay (ms)                     | `300000`                 | No       |

### Deploy

1. Initialize Terraform:

```bash
cd terraform
terraform init
```

2. Plan the deployment:

```bash
terraform plan
```

3. Apply the infrastructure:

```bash
terraform apply
```

4. Get the API Gateway URL and API Key:

```bash
terraform output apigw_url
terraform output api_key_value
```

### Infrastructure Components

The Terraform configuration creates:

- **VPC** with public/private subnets
- **DynamoDB Tables** (events, inventory, tickets) with KMS encryption
- **SQS Queue** for asynchronous processing
- **ECS Fargate** service with auto-scaling
- **Application Load Balancer** with health checks
- **API Gateway** with REST API and API key authentication
- **KMS Key** for encryption
- **IAM Roles** with least privilege permissions
- **CloudWatch** log groups

### Security Features

- KMS encryption for DynamoDB tables
- API key authentication for API Gateway
- IAM roles with minimal permissions
- Private subnets for ECS tasks
- Security groups with restrictive rules
- CORS configuration for web security

# Terraform which creates resource on AWS.

![fiverr-terraform-web-app](https://user-images.githubusercontent.com/44109187/91877292-032a8300-eca8-11ea-949a-f2606820ec03.png)

## Prerequisites
- Terraform v0.12.6
- aws v2.53

These types of resources are supported:

- VPC
   - Public Subnet
   - Private Subnet
   - Availability Zones
   - Internet Gateway
   - NAT Gateway

- Elastic Compute Cloud (EC2)
   - Launch configuration
   - Autoscaling Group
   - Elastic Block Storage (EBS) 

- Relational Database Service (RDS)
   - DB subnet group
   - DB parameter group
   - DB option group

- Security Groups
   - SSH
   - HTTP
   - HTTPS
   - MYSQL

- Elastic Load Balancer

## Requirement

- AWS Account
   - IAM Permissions to create services.
   - AWS credentials (Programmatic).
   - Configure AWS Profile default paths: `~/.aws/credentials`
   - GitHub Personal Access Token

```
[non-production]
aws_access_key_id=exmaple-access-key
aws_secret_access_key=example-secret-key
```

## Usage

- Create GitHub Personal Access Token

```
GitHub Profile => Settings => Developer settings => Personal access tokens => Generate new token => Check `repo` (Full control of private repositories)
```

- Create the `Kay Pairs` on AWS Console, To attach an EC2 instance for the access server

```
AWS Console => EC2 => NETWORK & SECURITY => Key Pairs
```

- Clone this repository and go to into directory

```
git clone git@github.com:kawinpromsopa/fiverr-terraform-web-app.git
```

- Update the new values and put the GitHub access token for creates resource into `workspace/non-production.tfvars`

- Terraform initial the modules

```
terraform init
```

- Create the terraform workspace to map the AWS Profile, Example following below:

```
$ cat `~/.aws/credentials`

[non-production]
aws_access_key_id=exmaple-access-key
aws_secret_access_key=example-secret-key

$ terraform workspace new non-production
$ terraform workspace select non-production 
```
NOTE IMPORTANT: The terraform workspace MUST be matched which named an AWS Profile Environment.

- Terraform apply to create all resources

```
$ terraform apply --var-file="./workspace/non-production.tfvars"
```

- Terraform destroy to delete all resources

```
$ terraform destroy --var-file="./workspace/non-production.tfvars"
```

- Terraform output, Will put the outputs resource information such as `elb_dns_name`, `db_instance_endpoint`. When the resource has created.

- Secure Shell (SSH) to instance server

```
ssh -i "key_pair_name.pem" ubuntu@<INSTANCE_IP_ADDRESS>
```

# Terraform CheatSheet

A comprehensive guide covering essential Terraform commands and configurations for infrastructure as code (IaC).

## Table of Contents

- [Installation & Setup](#installation--setup)
- [Initializing Terraform](#initializing-terraform)
- [Providers](#providers)
- [Variables](#variables)
- [State Management](#state-management)
- [Resource Management](#resource-management)
- [Modules](#modules)
- [Provisioners](#provisioners)
- [Terraform Workspaces](#terraform-workspaces)
- [Remote Backends](#remote-backends)
- [Security Best Practices](#security-best-practices)

## Installation & Setup

Install Terraform:

```bash
download Terraform from https://www.terraform.io/downloads.html
unzip terraform.zip
sudo mv terraform /usr/local/bin/
```

Verify installation:

```bash
terraform -v
```

## Initializing Terraform

Initialize Terraform in a project directory:

```bash
terraform init
```

Reinitialize the configuration and re-download modules:

```bash
terraform init -upgrade
```

## Providers

Define a provider in Terraform:

```hcl
provider "aws" {
  region = "us-west-1"
}
```

List required providers:

```hcl
terraform providers
```

## Variables

Define a variable:

```hcl
variable "instance_type" {
  type    = string
  default = "t2.micro"
}
```

Use a variable in a resource:

```hcl
resource "aws_instance" "example" {
  instance_type = var.instance_type
}
```

Pass a variable file:

```bash
terraform apply -var-file="vars.tfvars"
```

## State Management

Show current state:

```bash
terraform show
```

Manually refresh state:

```bash
terraform refresh
```

Save state to a file:

```bash
terraform state pull > state.json
```

## Resource Management

Format Terraform code:

```bash
terraform fmt
```

Validate Terraform configuration:

```bash
terraform validate
```

Plan infrastructure changes:

```bash
terraform plan
```

Apply changes:

```bash
terraform apply
```

Destroy resources:

```bash
terraform destroy
```

## Modules

Create and use a module:

```hcl
module "web_server" {
  source = "./modules/web"
}
```

List modules:

```bash
terraform modules list
```

## Provisioners

Define a provisioner for an EC2 instance:

```hcl
resource "aws_instance" "example" {
  provisioner "local-exec" {
    command = "echo Instance created!"
  }
}
```

## Terraform Workspaces

List workspaces:

```bash
terraform workspace list
```

Create a new workspace:

```bash
terraform workspace new dev
```

Switch workspace:

```bash
terraform workspace select dev
```

## Remote Backends

Configure an S3 backend:

```hcl
terraform {
  backend "s3" {
    bucket = "my-tf-state"
    key    = "terraform.tfstate"
    region = "us-east-1"
  }
}
```

Migrate to a backend:

```bash
terraform init -migrate-state
```

## Security Best Practices

- **Use remote state storage** to avoid losing state files.
- **Enable state file encryption** when using remote backends.
- **Use `terraform plan` before applying changes** to review modifications.
- **Restrict provider credentials** to least privilege.
- **Avoid storing secrets in code**; use Vault or AWS Secrets Manager.
# terraform-aws-ec2-example


```markdown
# Terraform AWS EC2 Example

This repository contains a basic Terraform configuration for provisioning an AWS EC2 instance along with a security group. It demonstrates how to use Terraform to manage AWS infrastructure.

## Prerequisites

- [Terraform](https://www.terraform.io/downloads) installed
- AWS account and credentials set up (use `aws configure` to set up your credentials)
- [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html) installed (optional, but useful for managing your AWS environment)

## Usage

### 1. Clone the repository:

```bash
git clone https://github.com/your-username/terraform-aws-ec2-example.git
cd terraform-aws-ec2-example
```

### 2. Initialize Terraform:

```bash
terraform init
```

This will download the necessary provider plugins.

### 3. Apply the configuration:

```bash
terraform apply
```

You will be prompted to confirm the changes. Type `yes` to provision the EC2 instance and security group in AWS.

### 4. Verify the resources in the AWS Console:

Go to the [AWS Console](https://aws.amazon.com/console/) and verify that the EC2 instance and security group have been created.

### 5. Destroy the resources:

When you are done, run the following command to clean up the resources:

```bash
terraform destroy
```

## Terraform Configuration

Below is the Terraform code used to create an AWS EC2 instance and a security group:

```hcl
# Configure the AWS provider
provider "aws" {
  region = "us-west-2"
}

# Create a security group to allow SSH and HTTP
resource "aws_security_group" "example_sg" {
  name        = "terraform-example-sg"
  description = "Allow SSH and HTTP traffic"
  
  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}

# Create an EC2 instance
resource "aws_instance" "example_instance" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"

  security_groups = [aws_security_group.example_sg.name]

  tags = {
    Name = "Terraform-Example-Instance"
  }
}
```

## License

This project is licensed under the MIT License.
```

### **5. Push `README.md` to GitHub:**

Once you’ve created the `README.md` file with the above content, commit and push it to GitHub.

1. **Stage and commit the file:**
   ```sh
   git add README.md
   git commit -m "Added README with Terraform AWS EC2 example"
   ```

2. **Push the changes:**
   ```sh
   git push
   ```


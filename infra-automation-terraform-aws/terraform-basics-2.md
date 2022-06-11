# Terraform Basics 2

## Separating File Base on Concern

You can have many file as your terraform config. Most common one are

- provider.tf, to store related provider value
- vars.tf, to store variable value
- terraform.tfvars, to store secret keys (dont forget to ignore it in git)
- instance.tf, resource related

## Software Provisioning

- You can create your own AMI
- Boot standarized AMI and install software or configuration with file uploads, remote exec, or tool like chef puppet ansible

- Chef is integrated on Terraform (we can add chef statement)

Example upload file and execute file

```tf
resource "aws_key_pair" "my_key" {
  key_name = "mykey"
  public_key = "ssh-rsa my-pub-key"
}

resource "aws_instance" "example" {

  key_name = ""

  provisioner "file" {
    source = "app.conf"
    destination = "/path/script.sh"
    connection {
      user = var.instance_username
      private_key = file(var.path.to.private)
    }
  }

  provisioner "remote-exec" {
    inline = {
      "chmod +x /opt/script.sh"
      "/opt/script.sh --help"
    }
  }
}
```

## Outputting Attributes

Use output to display attributes from your AWS resource or provider

```
output "ip" {
  value = aws_instance.example.public_ip
}
```

Use attributes in script

```
resource "aws_instance" "example" {
  ami = ""
  instance_type = "t2.micro"
  provisioner "local-exec" {
    command = "echo ${aws_instance.example.private_ip}"
  }
}
```

## Terraform State

- Terraform keeps remote state (ip, resource variables, etc) of infrastructure
- Store on file called terraform.tfstate
- Backup can be found in terraform.tfstate.backup
- When we execute `terraform apply`,  it will create a backup state and remote state.
- This is how terraform keeps track of remote state


```
## backend.tf

terraform {
  backend "s3" {
    bucket = "mybucket"
    key = "terraform/myproject"
    region = "eu-west-1"
  }
}
```

When using s3 its best to configure the aws credentials

```bash
$ aws configure

```

And then run

```
$ terraform init
```

it avoids having to use git to know the cahnge.

You can specify a read-only remote store directly in `.tf` file

```
data "terraform_remote_state" "aws-state" {
  backend = "s3"
  config = {
      bucket = "bucket-name"
      key = "terraform.tfstate"
      access_key = var.AWS_ACCESS_KEY
      secret_key = var.AWS_SECRET_KEY
      region = var.AWS_REGION
    }
}
```

## Data Sources

Data source provide dynamic information. 

- list of AMI
- list of API (public or private)

Example usage

- filtering traffic by IP


```
data "aws_ip_ranges" "european_ec2" {
  regions = ["eu-west-1", "eu-central"]
  services = ["ec2"]
}

resource "aws_security_group" "from_europe" {
  name = "from_europe"

  ingress {
    from_port = "443"
    to_port = "443"
    protocol = "tcp"
    cidr_blocks = ["${data.aws_ip_ranges.european_ec2.cidr_blocks}"]
  }

  tags {
    CreateDate = "${data.aws_ip_ranges.european_ec2.create_date}"
    SyncToken = "${data.aws_ip_ranges.european_ec2.sync_token}"
  }
}
```

## Template Provider

- Template provider help creating custom configuration file
- We can build template based on variables
- The result is a string that can be used as a variable in terraform

Create template file (.tpl)

```
## init.tpl

#!/bin/bash

echo "database-ip = ${myip}" >> /etc/myapp.config
```

```

data "template_file" "my_template" {
  template = "${file("templates/init.tpl)}"

  vars {
    myip = "${aws_instance.database1.private_ip}"
  }
}
```

Use my template resource when creating new instance

```
resource "aws_instance" "web" {
  user_data = data.template_file.my_template.rendered
}
```

Starting from 0.12 onwards 


```
resource "aws_instance" "web" {
  user_data = templatefile("templates/init.tpl", {
    my_ip = aws_instance.database1.private_ip
  })
}

## or using locals

locals {
  web_vars = {
    my_ip = aws_instance.database1.private_ip
  }
}

resource "aws_instance" "web" {
  user_data = templatefile("templates/init.tpl", locals.web_vars)
}
```

## Other provider

- Terraform is tool to manage infrastructure resources
- GCP, Azure, Heroku
- VMWare
- Datadog
- Github
- Mailgun
- DNSSimple

## Modules

- You can use modules to organize terraform
- Modules are just another terraform configuration

1. Use module form git/hub

```
module "git-module" {
  source = "github/repo/module/terraform"
}
```

2. Local folder

```
module "git-module" {
  source = "./module-example"
}
```

## Terraform command overview

- Terraform focuses on resource definition

```
$ terraform apply # applies state
$ terraform destroy # destroy infra
$ terraform fmt # format terraform file
$ terraform get # downlload and update modules
$ terraform graph # create visual representation
...

all other can be find on terraform --help
```

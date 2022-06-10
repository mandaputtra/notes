# Terraform Basics

Terraform using HCL (HashiCorp Configuration Language)

## Terraform Basics

### Defining variables

```tf
variable "myvar" {
  type = string
  default = "hello terraform"
}

variable "myMap" {
  type = map(string)
  default = {
      0 = "value"
  }
}

variable "myList" {
  type = list
  default = [1,2,3,4]
}
```

Running it

```ts
❯ terraform console
> var.myvar
"hello terraform"
> "${var.myvar}"
"hello terraform"
> 
```

### Resources / Provider

```tf
provider "aws" {

}

variable "AWS_REGION" {
  type = string
  default = "eu-west-1"
}

variable "AMIS" {
  type = map(string)
  default = {
    eu-west-1 = "my ami"
  }
}

resource "aws_instance" "example" {
  ami = var.AMIS[var.AWS_REGION]
  instance_type = "t2.micro"
}

```

`provider` used to specify what provider you're using either AWS, Docker, etc.

`resource` used to specify what resource are your infrastructure need


### Planning and Applying

```tf
$ terraform init # applying provider - setup installing
$ terraform plan # check your plan is correct or not, show what terraform does
$ terraform apply # apply configuration
```

## AWS Setup

- Opening AWS account.
- Configure IAM User as an Admin
- Copy Access Key ID and Secret Key ID form the User

## Spinning Up an Instance

AMI Locator : Choose the closest one https://cloud-images.ubuntu.com/locator/ec2/

```tf
provide "aws" {
  access_key = ""
  secret_key = ""
  region = "ap-shouteast-3"
}

resource "aws_instance" "example" {
  ami = "ami-0e1af156739c38b84"
  instance_type = "t2.micro"
}
```

```tf
$ terraform init
$ terraform apply

$ terraform destroy # destroy instance
```


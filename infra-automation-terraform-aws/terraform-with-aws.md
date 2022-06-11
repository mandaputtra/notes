# Terraform in AWS

## VPC

- Virtual Private Network
- VPC Isolates instance in network level. Picture it as internet cafewith all the computer as an instance
- It's best practice to use VPC
- An instance lauch in one VPC can never communicate with an instance in an other VPC using their private IP
- Can communicate using public IP but not recommended
- Link other VPC with peering
- On AWS you start by create your own VPC
- VPC had subnets, most subnets used are 10.0.0.0/16

```
resource "aws_vpc" "main" {
  cidr_bloc = "10.0.0.0/16"
  instance_tenancy = "default"
  enable_dns = "default"
  
  tags = {
      Name = "main"
  }
}

# subnets

resource "aws_subnet" "main_public1" {
  vpc_id = aws_vpc.main.id
  cidr_bloc = "10.0.0.0/24"
}

resource "aws_internet_gateway" {
  vpc_id = aws_vpc.main.id

  tags {
    Name = "main"
  }
}

# route table
resource "aws_route_table" "main_public" {
  vpc_id = aws_vpc.main.id
  route {
    cidr_bloc = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.main-gw.id
  }
}

# route associtions public, to expose to public internet
resource "aws_route_table_association" "main-public-1-a" {
  subnet_id = aws_subnet.main_public1.id
  route_table_id aws_route_table.main-public-1.id
}
```

- Nat gateway can be used to expose instance to public internet

## Spinning up EC2 with VPC

- security group is like firewall
- you can specify ingress (incoming) and egress (outgoing) traffic riles

If you want only access SSH (port 22) you can do that with these rules : 

- Allows ingress port 22 on IP address range 0.0.0.0/0 (all IPs)
- best practice to only allow your own IP
- allow all outgoing traffic from the instance to 0.0.0.0/0 (all IP, everywhere)

https://github.com/wardviaene/terraform-course/tree/master/demo-8

## EBS Volume

Elastic Block Storage

- t2.micro EC2 instance automatically adds 8GB EBS
- Some instance had local storage, will lost if instance terminate

https://github.com/wardviaene/terraform-course/tree/master/demo-9

There are a lot of storage type on AWS

https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volume-types.html

## Userdata

Userdata could be used at *launch*

- Install extra software
- Prepare instance to join a cluster
- execute commands
- only execute during creation of instance

```
user_data = "<place your scriot here>"
```
https://github.com/wardviaene/terraform-course/tree/master/demo-10

## Static IP, EIP, and Route53

- Private IP address will be auto-assigned to EC2 instance
- Every subnets has its own range
- By specifying private IP, you can make it persist

EIP

- To use public IP address you can use EIP

```
resource "aws_eip" "my_ip" {
  instance = aws_instance.example.id
  vpc = true
}
```

Route53

- Typically you'll use hostname
- You can host domain with Route53
- Need registered domain first

https://github.com/wardviaene/terraform-course/tree/master/demo-11

## RDS (Relational Database Services)

Managed database solution

- replication
- snapshots
- security updates

Type :

- Oracle
- MySQL
- MariaDB
- PostgreSQL

Steps:

- Create subnets group
- parameter group
- RDS will put in private ip

```
security_group = [aws_security_group.example.id]
```

https://github.com/wardviaene/terraform-course/tree/master/demo-12

## IAM (Identity & Access Management)

Create roles and users

- Users can have groups
- Users can authenticate, using OAuth or etc
- It can also attached with an instance

https://github.com/wardviaene/terraform-course/tree/master/demo-13

https://github.com/wardviaene/terraform-course/tree/master/demo-14

## Autoscaling

Automatically add and remove instances when some threshold reached

You need 2 instances at least to do autoscaling

https://github.com/wardviaene/terraform-course/tree/master/demo-15

## ELB (Elastic Load Balancer)

ELB automatically distributes incoming traffic

ELB can also be used as SSL terminator, you dont have to encrypt/dcrypt traffic

Same as Nginx or Haproxy, but AWS provide the abstraction for services

```
resource "aws_elb" "my_elb" {}
```

https://github.com/wardviaene/terraform-course/tree/master/demo-16

## ALB (Application Load Balancer)

Rule based load balancing.

```
resource "aws_alb_target_group_attachment" "my_attachment" {}

resource "aws_alb_listener" "my_listener" {}
```

You can specify target instance with ALB based on path that are accessed by users.

```
condition {
  field = "path-pattern"
  values = ["/static/*"]
}
```

## Elastic Beanstalk

- PaaS solution
- It's platform where you launch your app on without having to maintain infrastructure
- You responsible for the EC2 instances but AWS will provide updates (maunal or automatically)
- It's like Heroku, but with less automation

https://github.com/wardviaene/terraform-course/tree/master/demo-17



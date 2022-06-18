# Docker on AWS

- We are running AWS guest operating system that AWS provided
- You need a `Dockerfile` to use docker on AWS its somewhat same as running on your Amazon Linux
- Step: Build - Push - Run
- Amazon ECR is where we push our docker registry build
- To run we need to run it on ECS

## ECS


- ECS EC2 Container. will manage docker containers
- Once ECS online then we could run our docker app
- Before the docker app can be launched a task definition need to be provided
- The task definition describes what docker container to be run on the cluster
    - Specifies docker image on the ECR
    - Max CPU Usage max memory usage
    - Whether containers should be link to other container
    - Env

- Service definition is going to run specific amount of container based on the task definition 
- Service is always running if the container stop, it will be restarted
- You can put ELB

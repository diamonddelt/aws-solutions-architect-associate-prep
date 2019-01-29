# ECS

ECS is short of Elastic Container Service, which is the AWS managed service to automate working with containers, such as Docker or LXC containers.

It can store the container images in either DockerHub or ECR (Elastic Container Registry). ECR support private Docker repositories in conjunction with IAM for authentication.

ECS allows you to auto-scale the number of container instances to a specific number, similar to `Kubernetes`


## Task Definitions

A task definition is required to run Docker containers in ECS, and it's just a json file which describes one or more containers that form the application (think docker-compose file).

Parameters to include in a task definition include:
  
- Which container image to use with the task (such as alpine:latest, for example)
- How much CPU and memory to allocate to each container
- Whether containers are linked together in a task
- The Docker networking mode to use
- What if any ports are mapped from the host to the container instance
- Whether the task should continue to run if the container finishes or fails
- The command to run the container when the task is started
- Environment variables to pass to the container when the task starts
- Any data volumes that should be used with the containers in the task
- What IAM role your tasks should use for permissions (if they modify other AWS resources)

## Types of Scheduling

- Service scheduling - ensures that the specific number of tasks are constantly running and reschedules tasks when they fail (for example, if the container instance fails)
- Custom scheduling - you can create your own scheduler, or leverage third-party schedulers such as `Blox`

## The ECS Container Agent

- This agent can be loaded on an EC2 instance
- Linux-based
- Does not work on Windows, but works on most linux distros

## ECS Security

- EC2 instances use an IAM role to access ECS
- ECS tasks use an IAM role to access other AWS resources
- Security Groups attach at the instance level (i.e. the host, not the task or container)
- You can access and configure the OS of the EC2 instances in the ECS cluster (Because an ECS cluster is just a group of EC2 instances acting as Docker container hosts)

## Limits

Soft Limits:

- Clusters per Region (default = 1000)
- Instances per Cluster (default = 1000)
- Services per Cluster (default = 500)

Hard Limits:

- One load balancer per Service
- 1000 tasks per Service (`desired count`)
- Max. 10 containers per Task Definition
- Max 10 tasks per instance (`host`)
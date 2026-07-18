# Containers
- In AWS we have two ways of containerzation they are AWS ECS and EKS

## Container Orchestrators

- Container Orchestrators are the **brains of a containerized environments**

## Resposibilites

- Deploying containers across all available servers
- Load balencing request to containers
- Providing container to containers
- Restarting failed containers
- Moving containers when hosts fail
- Best open source container Orchestrators are
kubernetes, APache Mesos and AWS ECS

## Elastic Container Service (ECS)

- Fullly managed containers orchestration service that helps to scale and manage the containerized applications
- ECS is completely work inside the AWS if you plan for migratin to another cloud that will be challenge

> **Note:** Containers runs on the EC2 instance or Fargate not on ECS. THe ECS just manage the containers

---

# EKS Elastic kubernetes service

## Kubernetes

- It is open source container orhes
- It has **two types of nodes Control Plane and Worker**
- **Control Plane Node**
    - IT manage of the clusters
    _ it will watch over cluster and make sure cluster is kept in a working state
- **Worker Node**
    - It is responsible for actually running the containezed workloads

---    

## EKS
- Normally users in kubernetes need to manage both control plane and worker nodes.
- managing both is diffecult
- To short it down AWS EKS comes in
- EKS **mamges the control plane node** it will scale the things by their side.
- Users are still resposnible for **managing worker nodes **


## benefits of EKS
- Runs and scale control plane across multiple AZ.
- Scales control plane based on the load
- CAn integreate with other AWS services

---

## ECS vs EKS
- ECS is prior to AWS so migrating to other cloud it will be difficult
- EKS If you have more aws services you configre with your cluster then it will be hard to move to another provider
- ECS is **simple architecure** simple API easy to work
- Kuberntees is **complex part** to use the EKS you need to know the kubernettes also.
- Pricing
    - ECS Pricing is no cost for control plane, only cost applies to infra runiing application EC2
    - EKS pricing - more expensice, you have to pay for control-plane and worker nodes
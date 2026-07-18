# Core AWS Services Networking
---

# Virtual Private cloud

- VPC is sercure,isolated network hosted within the AWS.
- Isolate means if you have AWS account has services and another person will have services. You Both will have isolated VPC network so they wont talk each other
- VPC gives full control of the networking in the cloud for the customers.
- When you going to create the VPC you will set the CIDR block something 192.168.0.0/16
- What is means any resource that you are going to deploy within the VPC must be within the CIDR range
- CICR block size can be anywhere from /16 to /28
- 192.168.0.0/16 means range will start from 192.168.0.0 to 192.168.255.255

## Note

- It dosent mean that for one custmer there will be one VPC. Not Exaclty
- One customer can have many VPC it depends on their infra
- Like if you have Deployymnet,Staging Production etc. For these each env you can create the seperate VPC.

## VPC and Regions

- For an One Region we will have one VPC alone.
- If you have multiple VPC within one region.
like stage,production(env) by default vpc wont comuication each other you cant access each other.
- You need to do configuration to commuincate

## Types

- Vpc have two types.
- **Default** and **Custom**
- Every account has the default VPC in each region
- In default VPC, AWS will provide you all the basic configuration, you dont have to maintain anything for quick access.
- Where Custom VPC is every confugration you only need to do.

## Default VPC

- One defaul VPC per region
- The default VPC has the /16 CIDR block like 172.31.0.0/16 (65,536 addresses)
- Inside default VPC we have default vpc isndie the vpc we have **default subnets** for each AZ
- Subnets has address of /20 like 172.31.0.0/16 (4,096 addresses)
- If we have two AZ, we will have two seperate subnets.
- With default VPC the **Internet gateway automatically attached** to the VPC.
- The IG points the route as 0.0.0.0/0 which means all the **default subnets will be accessible from the internet**
- You will get default security group
- You will get default network acccess control list


---

# Subnets

- The Subnets is a group of ip addresses.
- The subnets implemented  within a **single AZ**
- So subnet going to determine where you deploy the resources and what AZ is fall in based on the subnet you associated with
- Subnet have two types private and public
- Private is restriceted from the internet no body can access it. (We can use this as back end server,database). This is default type when you creae the subnet
- Public is opposite it is accesseble from the internet (We can use this web application)
- Subnet is group of ip address right we make sure that this also falls under the VPC CIDR block range

## Note

- The subnet in cloud vs own data center where the AWS will reserve couple of extra IP address  and cannot be used
- The first 4 ip address and last ip address of subnet are reserved and cannot be used.

## Example
- If you have 192.168.10.0 means
- 192.168.10.0 will goes for NEtwork Address (reserved)
- 192.168.10.1 to 192.168.10.3 These 3 range ip address are reserved for AWS
- Last IP address 192.168.10.255 is reserved as the broadcast address

---

# Internet Gateway (IG)

- WHen you create the SUbnet by default it will create as private network.
- If you want to change private to public we need Internet Gateway
- The IG is **mapped with VPC level** not subnet level. and subnets in a VPC can able to commuincate to internet and from other internet can commuiate to your subnet (vice versa)
- So the IG **determine that subnet is public or private**
- there is another tool which we can make subnet private to public is **NAT Gateway**

---

# Nat Gateway
- IT is little bit different from IG
- NAT is a connection must be **initialed within the VPC**
- NAT gives our  internal resouce to commucate with internet but they have to initiate the connections.
- So if the Internet tries to contact our resouce it will blocks but if the resources connect to the ohter internet means it allows
- SO the diff between NAT and IG is the **IG allows either side to initiare the connection but NAT ecpevts the connection from the resouces to internet alone**


## How it works

- Any public subnets which has the IG access is the public subnet can comuincate to internet
- But if you want to use NAT you still need an internet gateway,but what is happening is **you will be deploying the NAT Gateway to public subnet** which is going to give access to the IG.
- And your private subnet anyhting wants to commicate to internet, the send the request to the NAt gateway, That NAt gatewayt send request to the IGand the request will go out to intenet and you will get the response in opposite direction.

> **Note:** If you going to use Nat gatway still you need internet gateway to commicate the internet..

## Example Real-Time Scenario: Internet Gateway vs NAT Gateway

## Scenario

Suppose your company has a Spring Boot backend application deployed on AWS.

The application needs to:

- Call Stripe Payment API
- Send emails using Gmail API
- Send SMS using Twilio
- Download OS updates
- Pull Docker images
- Access GitHub repositories

These operations require **outbound internet access**.

---

## Option 1: Internet Gateway (Public Subnet)

```text
                Internet
                    │
            Internet Gateway (IGW)
                    │
              Public Subnet
                    │
             Spring Boot EC2
```

### Communication

```text
Spring Boot EC2  ---> Internet      ✅
Internet         ---> Spring Boot   ✅
```

### Use Case

Choose this when your application **must be directly accessible from the internet**, for example:

- Web Server
- Bastion Host
- Public API Server (less common in production)

### Problem

Because the EC2 instance has a **public IP**, anyone on the internet can attempt to connect to it.

Even with Security Groups protecting it, the server is still exposed to:

- Port scanning
- SSH attacks
- Vulnerability scanning
- Brute-force login attempts

---

## Option 2: NAT Gateway (Private Subnet)

```text
                Internet
                    │
            Internet Gateway (IGW)
                    │
              NAT Gateway
                    │
             Private Subnet
                    │
             Spring Boot EC2
```

### Communication

```text
Spring Boot EC2  ---> Internet      ✅
Internet         ---> Spring Boot   ❌
```

### Why?

The Spring Boot application can:

- Call Stripe API
- Send emails
- Download updates
- Pull Docker images
- Access GitHub

But no one from the internet can directly connect to the EC2 instance because it has **no public IP**.

---

## Why Companies Prefer NAT Gateway

In production, companies usually do **not** expose application servers directly to the internet.

Instead, they use an **Application Load Balancer (ALB)**.

```text
                    Users
                      │
                  Internet
                      │
          Internet Gateway (IGW)
                      │
        Application Load Balancer
                (Public Subnet)
                      │
        ----------------------------
        │                          │
   Spring Boot EC2            Spring Boot EC2
   (Private Subnet)           (Private Subnet)
        │                          │
        └──────── NAT Gateway ─────┘
                      │
                  Internet
```

### Request Flow

1. Users send requests to the **Application Load Balancer (ALB)**.
2. The ALB forwards requests to Spring Boot EC2 instances in **private subnets**.
3. The Spring Boot application processes the request.
4. If needed, it calls external services (Stripe, Twilio, Gmail, etc.) through the **NAT Gateway**.
5. The response is returned to the user through the ALB.

---

# Virtual Private Gateway

- THis is used when you want to connect to any private resource in AWS. 
- It will be achived through the secure VPN connections
- It is the secure connection which the data will be encrypted to pass over the internet

## Scenario
- Imagine if you have an private subnet that wont have any internet access itself
- But you want to conncet securely to that private subnet due to some reasons like monitoring, any configuration changes etc

> **Notes:** Even though it is secure the connection between external data center to our private center is happening in encrypted way, it is **travelling through the internet**.

---

# Direct Connect

- This is the other way of connection the external data center (servers) to commiacte with private subnets.
- What is happening is you as the customers will actually have to go this **specific location called DX location or Direct Connect**
- In location what you have to do is physically connect your router or something to the specific location.
- So what does the location do is, it has high speeed connection to AWS Regions. And it makes the secure connection to your AWS.

---

# Firewalls

- Imagine we have an server listening on 443
- If user send request to the server he will mention the 443 and send the request
- and the server will return to the user
- In between the travel how will manage that only travel needs to go to 443 port only not other ports are applicable.
- So we want to block the other traffics. That tis the job of firwwalls
- SO firewall will protect our server will set of rules.
- There are two types **inbound** and **outbound**

## Inbound

- Inbound rules are what traffic allowed to enter to the device

## Outbound

- This rules determine that what traffic pur server is allowed to send out

## Stateless firewalls

- Stateless firwalls must be configured to allow both inbound and outbound
- It donwt not remember what request and response.

## Stateful firewalls

- It is inteligent enought to understand which request and response are part of the same conection.
- If request is permited the response is automatically permited in statefull firewall

---

# AWS firewalls

## Network Access Control List (NACL)

- NACL are stateless firewalls, so rules must be set for the inbound and outbound rules
- NACH filters traffic entering and leaving the subnet
- NACL do not filter traffice within the subnet

## Security Groups

- The Security groups are statefull so we will configrue only the request the response is automatically sent
- For individual resources in AWS has the secirty group
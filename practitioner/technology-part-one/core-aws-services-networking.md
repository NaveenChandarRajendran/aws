# Core AWS Services Networking
---

## Virtual Private cloud

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

---

## Subnets

- The Subnets is a group of ip addresses.
- The subnets implemented  within a single AZ
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

## Internet Gateway (IG)

- WHen you create the SUbnet by default it will create as private network.
- If you want to change private to public we need Internet Gateway
- The IG is **mapped with VPC level** not subnet level. and subnets in a VPC can able to commuincate to internet and from other internet can commuiate to your subnet (vice versa)
- So the IG **determine that subnet is public or private**
- there is another tool which we can make subnet private to public is **NAT Gateway**

---

## Nat Gateway
- IT is little bit different from IG
- NAT is a connection must be **initialed within the VPC**
- NAT gives our  internal resouce to commucate with internet but they have to initiate the connections.
- So if the Internet tries to contact our resouce it will blocks but if the resources connect to the ohter internet means it allows
- SO the diff between NAT and IG is the **IG allows either side to initiare the connection but NAT ecpevts the connection from the resouces to internet alone**



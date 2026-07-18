# Elastic Compute 2

- In one phycial server of AWS can provide 100s to 1000s of instance to the customers using **Virtual machines**
- By using that we can use more mini instance(with OS) within a single aws phycial server
- The way we **isolate the ec2 is by using VPC**
- VPC is will make our **infrastrucutre too isolate even its all in single physical server of aws**

---

## Images - Amazon Machine Image (AMI)

- T0 use the OS in cloud we will use AMI here , unlike in physical server if you weant to install OS means you will have installer disk or bootable USB. But here its AMI images will take care
- So **AMI acts as installer disk for your EC2 instance**
- AMI is not only OS it has customize configuration things. 
    - Like Add applicatin source code, 
    - add dependies 
    - customize OS firewall

---

## Instance Types

- **General Purpose**
    - Provide a good balence of comute,memory amd network resouces
    - Can be used for diverse workloads.
    - Ideal for appliation that use resources in equal positions.

- **Compute Optimized**
    - Optiized for compute-heavy applicationns
    - Constains high-preformace CPU
    - IDeal for batch processing, machine learning and gaming servers.

- **Memory Optimized**
    - Deliver fast performance for memory intensice workloads
    - Suited for databases

- **Storage Optimized**
    - Optimized for workload that reuire high,sequntial rea and write access to large data sets on local storage
    - Can deliver very low latency systems

- **Acceleratled Computing**
    - Utilize the accelerators to perform expensive calcualtions.
    - Great for graphics  process and data pattern matching

---

## Instance pricing

- **On Demand Pricing**
    - Pay for how many hours your instance is live.
    - Only billed if you instance is running(Still charged for the strorage attched to instance)
    - Great for short-term,irreguar or unprectiable workloads
    - But we need to keep in mind Other customer EC2 isntance also run on shared hosts.

- **Spot Pricing**
    - Uses AWS's unused EC2 capacity at a heavily discounted price.
    - Can save up to **90%** compared to On-Demand pricing.
    - The **Spot Price** is the current price for using a Spot Instance.
    - AWS can reclaim the instance at any time if it needs the capacity for On-Demand customers.
    - AWS provides a **2-minute interruption notice** before stopping or terminating the instance.
    - Best suited for fault-tolerant workloads where interruptions are acceptable.

- **Reserve Pricing**
    - Reserving an instance for **1 to 3 years** and you will get **discounts**
    - WHen you deploy the on-demand instance with matching attributes as the reservation (instance type,region ,platform), it **will be charged as reserved price and not the default price** 
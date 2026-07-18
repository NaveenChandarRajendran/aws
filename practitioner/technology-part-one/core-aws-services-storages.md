# Types of Storage

```text
                    Storage
                      │
        --------------------------------------------------
        │                          │                     |
  Block Storage                File Storage          Object Storage
```
---

# Block Storage

- Amazon Elastic Block store (AMzon EBS)
- Elastic Block storage **breaks the data into blocks and then stores those blocks as seperate pieces**, each with uniqque identifier.
- The EBS valume is seperate to the EC2 instance.
- If EBS valume is specific to one AZ

## Usage 1

- It can presented to the **OS as Volume**. like how you will have local disk c,D, E and the volumes
- Then **OS will create the filesystem** on top of it.

## Usage 2
- It can be presented as **a hardrive**
- Block storage is **bootable** which means you can create install OS on it.

- Instance storages are removed when EC2 instance are stopped/started. Like const ,var will remove once we close the service and start it right

>  **Notes:** The EC2 and EBS must be present be present in the same availability zone.

---

# File storage
- AWS Elastic file system (AWS EFS)
- It stores the data in hierarchical structure of files and folders. Like how we will store data in computer
- File system **is accesible remotley**. So we can connect and create subdirectores and do the work like computers
- But it is **not bootable** so OS cant be installed.
- File system is accessible over teh network, so **it not means only one user can access the same data. Multiple users can access the same data at same time**

---

# Object Storage

- Aws S3
- Its like an drive or dropbox we we can store any kind of files
- it **does not have folder structure** Every file you upload is in same folder only
- It is great to save the media files and logs


# S3
- s3 is object storage you can store what ever data.
- We can drive the s3 with three classes
```text
                    Storage Class
                      │
        --------------------------------------------------
        │                          │                     |
    Data Access                Resiliency               Cost
```
## Standard Class
- The S3 will be handled with ,ulti AZ. If one AZ is failed means the S3 will avaiable with another AZ.
- It has 99.99999999999% (11 nines durability)
- It cost based on how much you store GB per month
- And amount of data that you send out that will be charged
as per the GB.
- S3 standard is the most expensive storage class due to data is available in mutli AZ and more fast

## Standard-IA

- If you have infrequent access you can use this class
- It has the same resilience which have in standard class like available in multi AZ, durability.
- The cost calulcation is also same as standard but  but it is little bit cheap than standard
- But It has the retrival fee minimun duration charge of 90 days will happen
- if we access data more freequently the this class will become more cost thatn the standard class.

## One Zone-IA

- This class is for those who does not want the resilence manner
- Means this class will store the data towards one AZ. So data wont be avaialble in multi AZ so you might loose the data.
- It also has the charged per data outbound and retrival fee of charge minimun 9- days and minial size charge of 128 KB per object
- But it is cheap than other two Standard class

## Glacier-Instant

-  It is cheap storage access.Where we can use it for rare retrivel systems
- It will work same as S3 standard, it has same performace like s3 standard and charged per GB. minimun duration of 90 days of retrival fee.
- Wehen though it is useed for rare access but the file will be available for instant

## Glacier-Flexible

- It is the cheap storage class than what ever learned in above mentioned storage class.
- THe retrivel of any file will let late. It is not instant avaiable storage class.
- It has same minimum duration cahrge of 90 days and charged per GB.
- It has options to retrival files 
```text
Bulk  ---> 5-12 Hours
Expedited ---> 1-5 minutes
Standard ---> 3-5 Hours
```

## Glacier Deep Archive

- This is most delayed access file. It is usefull for the file which is not need available instant may be not needed for while it is used for very very rare file access.
- It has same minimum duration cahegr of 90 days and charged per GB.
```text
Bulk  ---> 12 Hours
Standard ---> 48 Hours
```

## Intelligent-Tiering

- It manage the cost based on the user usability with AWS side analysis.
- AUtomatically reduce the cost storage costs by intelligenlty moving **the data to the most cost effective access tier**.
- But this has seperated charge aswell that is **monitoring/automation cost per 1000 objects**

> **Hint:** How to select the storage for our work is we need thing about the how much the data should be available and what is the purpose of that storage?
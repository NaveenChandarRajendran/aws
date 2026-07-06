# AWS Global Infrastructure

---

# Region

## Definition

An **AWS Region** is a geographical area that contains one or more **Availability Zones (AZs)**.

## Key Points

- AWS has Regions in many countries around the world.
- Each Region is **completely isolated** from other Regions.
- The **pricing** of AWS services varies between Regions.
- Not every Region offers every AWS service.
- You choose a Region based on factors such as latency, pricing, compliance, and service availability.

## Example

If your application users are mainly in **India**, you might deploy it in the **Mumbai Region (ap-south-1)** to reduce latency.

## Interview Question

### Why are AWS Regions isolated?

**Answer:**

Isolation improves fault tolerance. If one Region experiences a major outage, applications running in another Region remain unaffected.

---

# Availability Zones (AZ)

## Definition

An **Availability Zone (AZ)** is one or more data centers within an AWS Region.

Each Region contains **multiple AZs**, and every AZ has independent power, networking, and cooling.

## Key Points

- Every Region contains multiple Availability Zones.
- AZs are connected through **high-speed, low-latency networking**.
- Each AZ is physically separated from the others.
- Deploying resources across multiple AZs provides **High Availability** and **Fault Tolerance**.

## Example

Suppose your application is deployed in the **Mumbai Region**.

```text
Mumbai Region

├── AZ-1
│     └── EC2 Instance
│
├── AZ-2
│     └── EC2 Instance
│
└── Load Balancer
```

If **AZ-1** goes down, the **Load Balancer** redirects traffic to the EC2 instance running in **AZ-2**.

> **Note:** This failover happens only if your application is deployed across multiple AZs.

## Interview Question

### Why should we deploy applications in multiple Availability Zones?

**Answer:**

To achieve High Availability and Fault Tolerance. If one AZ fails, the application continues serving users from another AZ.

---

# Global CDN & Edge Locations

## Definition

An **Edge Location** is a site where AWS caches content closer to users.

Edge Locations are mainly used by **Amazon CloudFront**, **Route 53**, and **AWS WAF**.

## Why do we need Edge Locations?

Imagine your application is deployed in the **US Region**, but users access it from **India**.

Without Edge Locations:

```text
User (India)
      │
      ▼
USA Region
      │
      ▼
Response
```

The request travels a long distance, increasing latency.

With Edge Locations:

```text
User
   │
   ▼
Nearest Edge Location
   │
   ▼
USA Region (only if required)
```

Frequently requested content is served directly from the nearest Edge Location, reducing latency.

## Key Points

- Edge Locations are distributed across the world.
- They cache frequently accessed content.
- They reduce latency and improve response times.
- They are primarily used by:
  - Amazon CloudFront
  - Amazon Route 53
  - AWS WAF

## Interview Question

### Does an Edge Location store my entire application?

**Answer:**

No. Edge Locations mainly cache static content and frequently requested data. The main application continues to run in the AWS Region.

---

# Local Zones

## Definition

A **Local Zone** is an extension of an AWS Region that places AWS compute, storage, and other services closer to users.

## Why do we need Local Zones?

Some applications require **ultra-low latency**, such as:

- Online Gaming
- Video Rendering
- Machine Learning
- Media Production
- AR/VR Applications

If users are far from the parent Region, Local Zones reduce latency by bringing AWS resources closer to them.

## Key Points

- Local Zones are extensions of a parent AWS Region.
- They provide lower latency for nearby users.
- They support many AWS services such as EC2, EBS, and VPC.
- They are connected to their parent Region.
- AWS has fewer Local Zones than Edge Locations.

## Example

```text
Mumbai Region
      │
      ├── Local Zone (Chennai)
      └── Local Zone (Hyderabad)
```

Applications can run in the Local Zone while remaining connected to the parent Region.

---

# Local Zone vs Edge Location

| Feature | Local Zone | Edge Location |
|----------|------------|---------------|
| Purpose | Run applications closer to users | Cache content closer to users |
| Acts as | Extension of a Region | Global CDN Network |
| Supports Compute (EC2) | ✅ Yes | ❌ No |
| Supports Storage | ✅ Yes | ❌ No |
| Used by CloudFront | ❌ No | ✅ Yes |
| Used by Route 53 | ❌ No | ✅ Yes |
| Used by AWS WAF | ❌ No | ✅ Yes |
| Number of Locations | Limited | Hundreds worldwide |
| Connected to Parent Region | ✅ Yes | No |

---

# Quick Interview Summary

| Service | Purpose |
|----------|---------|
| Region | Geographical location containing multiple AZs |
| Availability Zone | Isolated data center within a Region |
| Edge Location | Cache content close to users using CloudFront |
| Local Zone | Extend AWS services closer to users for low latency |

---

# Easy Way to Remember

- **Region** → Country/Geographical Area
- **Availability Zone** → Data Center
- **Edge Location** → CDN Cache
- **Local Zone** → Mini AWS Region near users
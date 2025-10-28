- what is [[cloud computing]]? On-demand(access to a service or resource **whenever you need it**) delivery of IT resources over the internet with [[pay-as-you-go pricing]] (you only pay for what you use).
- You can deploy cloud resources in multiple ways: cloud, on-premises, and hybrid.
### **[[Cloud-Based Deployment]]**
- **Definition:** All resources (e.g., servers, storage, databases) are hosted in the cloud.
- **Use cases:**
    - Migrate existing on-prem resources to the cloud.
    - Build new cloud-native applications.
- **Example:** Hosting virtual servers and databases fully in AWS, Azure, or GCP.
- **Benefits:**
    - Scalability
    - Cost-efficiency (pay-as-you-go)
    - High availability
    - Managed services
---
### **[[On-Premises Deployment]]**
- **Definition:** Resources are hosted locally within an organization’s own data center.
- **Use cases:**
    - Organizations needing full control or very low latency.
    - Regulatory/compliance-driven environments.
- **Drawbacks:**
    - Limited scalability
    - Higher maintenance cost
    - Requires IT staff and infrastructure investment
- **Note:** Often uses virtualization to simulate cloud-like environments but lacks many cloud benefits.
---
### **[[Hybrid Deployment]]**
- **Definition:** Mix of on-premises infrastructure and cloud services working together.
- **Use cases:**
    - Gradual migration to the cloud
    - Keeping legacy apps on-prem while using the cloud for modern workloads
- **Example:** Keep a healthcare records system on-prem (for compliance) and use cloud for analytics.
- **Includes:**
    - **Hybrid cloud** (on-prem + cloud)
    - **Multi-cloud** (multiple cloud providers)
___
## **Benefits of the AWS Cloud**
#### **1. Pay-as-you-go**
- No upfront costs — pay only for what you use.
#### **2. Lower Costs**
- AWS’s scale leads to cheaper prices for everyone.
#### **3. Auto Scaling**
- Resources adjust automatically to demand — no over/underprovisioning.
#### **4. Faster Deployment**
- Launch apps in minutes — innovate and respond quickly.
#### **5. No Data Center Costs**
- No need to buy, run, or maintain physical servers.
#### **6. Global Reach**
- Deploy apps worldwide instantly using AWS infrastructure.
---
## **Introduction to AWS Global Infrastructure**
- **[[High availability]]** is all about making sure your applications stay accessible with minimal downtime.
- [[Fault tolerance]] takes it a step further by designing a system to continue to operate even if multiple components fail.
- [[AZ]] : availability zone
	- There are three or more AZs within a Region, for redundancy
	- not built right next to each other, (natural disaste = lose connectivity to everything in that AZ)
___
## The AWS Shared Responsibility Model
![[Screenshot_20250726_174756.png]]
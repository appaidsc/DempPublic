# 🌐 Networking Basics

| **Type**       | **Description**                                                                        |
| -------------- | -------------------------------------------------------------------------------------- |
| **Public IP**  | Used to access the Internet. Unique globally.                                          |
| **Private IP** | Used within your own local/private network. Not accessible directly from the Internet. |

---

## 📄 IPv4

IPv4 (Internet Protocol version 4) provides **4.3 billion addresses**.

Address format:  
`0.0.0.0 → 255.255.255.255`

| **Class**   | **Range (First Octet)** | **Purpose**            |
| ----------- | ----------------------- | ---------------------- |
| **Class A** | `0   - 127`             | Large networks         |
| **Class B** | `128 - 191`            | Medium-sized networks  |
| **Class C** | `192 - 223`           | Small networks         |
| **Class D** | `224 - 239`           | Multicasting           |
| **Class E** | `240 - 255`           | Experimental, reserved |

---

## 📄 IPv6

Newer version of IP with **128-bit addresses**.  
Provides an almost infinite number of addresses.

Example:  
`2001:0db8:85a3:0000:0000:8a2e:0370:7334`

---

## ☁️ VPC — Virtual Private Cloud

A **logically isolated section** of the cloud where you can launch your resources.  
You control your IP addressing, subnets, routing tables, and gateways within a VPC.

IPv4 subnets are defined as:


Where:
- Prefix Length → bits fixed for the network part.
- Remaining bits → number of hosts (IP addresses) available.

Example:  
`10.0.0.0/24`
- Total bits = 32
- Network bits = 24
- Host bits = 32 − 24 = **8**
- Number of addresses = 2⁸ = **256 addresses**

---

### 🔷 Example: `/20`
`10.0.0.0/20`
- Host bits = 32 − 20 = **12**
- Number of addresses = 2¹² = **4096 addresses**
- Typically decided/configured by a **solution engineer**.

---

# 🔷 Subnetworks

A **subnetwork (subnet)** is a smaller network carved out of a larger network.

Example:  
`192.168.0.0/24`
- Host bits = 8 → 2⁸ = 256 IPs.

If we split it into **2 subnets**, each will have 128 IPs:
- Subnet 1: `192.168.0.0/25` → 2⁷ = 128 IPs
- Subnet 2: `192.168.0.128/25` → 2⁷ = 128 IPs

---

# 📝 Reserved IPs in Every Subnet

In cloud environments (like AWS, GCP, Azure), **5 IPs in each subnet are reserved**, and cannot be used by your resources:

| **IP in Subnet**    | **Purpose**               |
|-----------------------|---------------------------|
| `.0`                 | Network Address          |
| `.1`                 | Default Gateway (router) |
| `.2`                 | Reserved for DNS         |
| `.3`                 | Reserved for future use  |
| `.255`               | Broadcast Address        |

So, in a subnet with 256 IPs, **only 251 are usable**.

---

## 📌 Notes

- Always account for the 5 reserved IPs when planning networks in the cloud.
- Public IPs cost more and are limited; private IPs are reusable within different networks.
- IPv6 is being adopted more widely because IPv4 addresses are running out.

---

## 🚀 Task Example

✅ Create a **VPC**  
✅ Then create **2 subnets**  
✅ Launch **one EC2 instance in each subnet**

---
# 📅 Day 4: Kubernetes — Auto Scaling

### 🚀 What is Auto Scaling?

Auto scaling is the ability of a system to automatically adjust the number of running resources (like pods, containers, or servers) based on the current workload or demand.
It helps maintain performance while optimizing costs.

---

## 📈 Types of Scaling

There are **two main types of scaling**:

---

### 1️⃣ Horizontal Scaling

* Adds **more instances (pods/containers/servers)** based on demand.
* When demand increases → more instances are added → **Scale Out**.
* When demand decreases → instances are removed → **Scale In**.
* Preferred in cloud-native environments like Kubernetes because it is more flexible and fault-tolerant.

---

### 2️⃣ Vertical Scaling

* Increases the **resources (CPU, RAM, etc.) of the existing instance** rather than adding more instances.
* When demand increases → the instance is replaced with a more powerful one → **Scale Up**.
* When demand decreases → the instance is replaced with a smaller one → **Scale Down**.

---

### 🚫 Drawbacks of Vertical Scaling

* Downtime is often required when replacing instances.
* There are physical limits to how much you can scale a single machine.
* Less fault-tolerant — if that instance fails, the service may be interrupted.

---

## 📋 AWS Auto Scaling Groups (ASGs)

When using AWS Auto Scaling Groups, you define:

* **Minimum number of servers**
* **Maximum number of servers**
* **Desired (default) number of servers**

AWS automatically ensures the number of running instances stays within the defined limits based on demand and health checks.

---

## 📊 Factors That Determine Auto Scaling

Several factors and metrics can trigger auto scaling, such as:

* CPU Utilization
* Memory Utilization
* Network Traffic
* Number of Requests
* Custom Metrics (e.g., queue length, response time)

These metrics are monitored continuously, and when thresholds are breached, scaling actions are performed.

---

## ⚡ Types of Scaling Strategies in Kubernetes

### Dynamic Scaling

* Kubernetes uses **Horizontal Pod Autoscaler (HPA)** to dynamically scale pods based on observed metrics (like CPU or memory usage).
* You can also configure **Vertical Pod Autoscaler (VPA)** for vertically scaling pod resources automatically.

---

## 📌 Notes

* Horizontal scaling is more commonly used in cloud-native applications because it offers better availability and reliability.
* Vertical scaling is simpler but less flexible and has limitations.
* Auto scaling helps save costs while maintaining optimal performance.

---

# ⚖️ Load Balancer

## What is a Load Balancer?
A **Load Balancer** is a service or device that distributes incoming network traffic (requests) across multiple servers or instances.  
It ensures that no single server is overwhelmed, and it improves application **availability, reliability, and performance**.

---

## 📝 Types of Load Balancer

1️⃣ **CLB → Classic Load Balancer (Absolute)**
- Legacy load balancer.
- Works at Layer 4 & basic Layer 7.
- Simple and easy to set up for basic applications.

2️⃣ **ALB → Application Load Balancer**
- Works at Layer 7 (Application Layer).
- Supports advanced routing:
  - Path-based
  - Host-based
  - Header-based
- Best for modern web apps and microservices.

3️⃣ **NLB → Network Load Balancer**
- Works at Layer 4 (Transport Layer).
- Ultra-low latency and high throughput.
- Best for high-performance, real-time applications.

4️⃣ **GLB → Gateway Load Balancer**
- Works at Layer 3 & 4.
- Useful for integrating with third-party virtual appliances (like firewalls, intrusion detection systems).
- Enables transparent deployment of security appliances.

---

# ☸️ Kubernetes

## What is Kubernetes?
**Kubernetes** (often abbreviated as K8s) is an **open-source container orchestration platform** that automates the deployment, scaling, and management of containerized applications.

Originally developed by **Google**, now maintained by the **Cloud Native Computing Foundation (CNCF)**.  
Each cloud provider offers its own managed Kubernetes platform.

---

## 🔍 What Does Kubernetes Do?
- Orchestrates and manages containers at scale.
- Automatically handles:
  - Deployment
  - Scaling
  - Networking
  - Storage
  - Failover
- Ensures high availability and reliability of containerized applications.

---

## 📄 Types of Kubernetes Platforms
- **On-Premises**: Install and manage it yourself on physical or virtual servers.
- **Cloud-Managed Services**:
  - AWS → EKS (Elastic Kubernetes Service)
  - Azure → AKS (Azure Kubernetes Service)
  - Google Cloud → GKE (Google Kubernetes Engine)
- Lightweight options:
  - Minikube (local testing)
  - MicroK8s (lightweight Kubernetes for development)

---

## 🐳 Docker & Kubernetes Workflow
```text
docker → create image → push to Docker Hub/ECR → deploy on Kubernetes cluster

---
# 📅 Day 6: Containers Orchestration & CloudFormation

---

## 🚀 Containers Orchestration

Container orchestration is the process of automating the deployment, scaling, and management of containerized applications.  
It ensures containers run reliably even in dynamic environments.

---

### 📦 What is a Container?
A container is a lightweight, standalone, executable package that includes everything needed to run an application — code, runtime, system tools, and libraries.

---

### 🔷 Key Features of Container Orchestration

1️⃣ **Automation of Deployment**
- Example workflow:
  - Provision EC2 instance
  - Install Docker
  - Pull the image from a registry
  - Build & run the container
- Orchestrators automate this entire process.

2️⃣ **Auto Scaling**
- Automatically adds or removes containers based on workload.

3️⃣ **Load Balancing**
- Distributes traffic evenly across multiple containers to ensure availability and reliability.

4️⃣ **Self-Healing**
- Automatically restarts failed containers and reschedules them on healthy nodes.

Popular orchestration tools:  
- Kubernetes
- Docker Swarm
- AWS ECS/EKS

---

## ☁️ CloudFormation & Infrastructure as Code

When managing cloud infrastructure at scale, manual setup becomes impractical and error-prone.  
This is where **Infrastructure as Code (IaC)** comes in — it allows you to define and provision infrastructure using configuration files.

---

### 🔷 Terraform & CloudFormation

- **Terraform** and **CloudFormation** are popular IaC tools.
- Terraform is open-source & cloud-agnostic.
- AWS **CloudFormation** is specific to AWS.

---

### 📄 AWS CloudFormation

CloudFormation helps you set up AWS resources automatically by defining them in a template file.

---

### 📝 Key Concepts

- **Template**
  - A blueprint describing the AWS resources you want to create.
  - Formats:  
    - JSON  
    - YAML (**preferred for readability**)

- **Stack**
  - A running instance of a CloudFormation template.
  - Represents a collection of AWS resources that you can manage as a single unit.

- **Rollback**
  - If a stack creation or update fails, CloudFormation can automatically revert to the previous stable state.

---

### 🌟 Why Use CloudFormation or Terraform?

- You can create **multiple EC2 instances in multiple AWS accounts** without manual intervention.
- Ensures consistency, repeatability, and faster deployment of infrastructure.
- Supports version control for infrastructure.

---







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


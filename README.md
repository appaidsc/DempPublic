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


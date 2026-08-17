# Project Report: Secure AWS Connectivity to Vendor A

**Author:** Adeniyi Abdulazeez (`hayzeddev123`)  
**Date:** August 2026

---

## 1. Introduction

Our organization needs to connect its Kubernetes applications to Vendor A. Vendor A requires all communication to use an **AWS Site-to-Site VPN** and allows access only from **one approved private IP address**.

---

## 2. Current Setup

The current infrastructure consists of:

* **Kubernetes Cluster** – Runs applications in a private subnet.
* **NAT Gateway** – Provides outbound internet access.
* **NGINX Ingress Controller** – Manages incoming traffic to Kubernetes services.

**The problem:**  
Kubernetes services can have different private IP addresses, making it difficult for Vendor A to whitelist a single source IP.

---

## 3. Proposed Solution

A dedicated egress path should be created for Vendor A traffic.

### Traffic Flow:

```
Kubernetes Pods
      ↓
Dedicated Egress / NAT
      ↓
Fixed Private IP
      ↓
Site-to-Site VPN
      ↓
Vendor A
```

**How it works:**

- Vendor A will whitelist the dedicated private IP.
- Routing rules will ensure that traffic destined for Vendor A goes through this path instead of the normal internet route.
- This provides a predictable and controlled source IP for all outbound connections to Vendor A.

---

## 4. Security

The following security measures will be applied:

* **Site-to-Site VPN** encrypts all communication between AWS and Vendor A.
* **Security Groups** and **Network ACLs** will allow only the required traffic.
* **VPC Flow Logs** and **Amazon CloudWatch** will be used for monitoring and auditing traffic.

These controls help ensure that only authorized communication reaches Vendor A and that the connection remains secure.

---

## 5. Conclusion

The proposed solution provides a **secure and controlled connection** between the Kubernetes cluster and Vendor A.

By using a dedicated egress path with a fixed private IP and routing Vendor A traffic through the Site-to-Site VPN, the organization can satisfy Vendor A’s IP whitelisting and security requirements while keeping the Kubernetes cluster private.

---

**End of Report**

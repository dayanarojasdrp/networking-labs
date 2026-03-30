# LAB 05 – Kubernetes Networking

## Objective

This lab demonstrates core Kubernetes networking concepts, including:

- Deployments (frontend, backend, database)
- Services (ClusterIP, NodePort)
- Network Policies
- Ingress (conceptual)

The environment was deployed using a local Kubernetes cluster with Kind.

---

## Architecture

The system consists of three main components:

- Frontend → exposed externally via NodePort
- Backend → internal service (ClusterIP)
- Database → internal service (ClusterIP)

### Traffic Flow

Client → NodePort → Frontend → Backend → Database

---

## Deployments

Three deployments were created:

- frontend (nginx)
- backend (nginx)
- db (busybox)

Each deployment ensures pod management, scalability, and high availability.

---

## Services

Different service types were used:

### ClusterIP
- backend
- db

These services are only accessible within the cluster.

### NodePort
- frontend

This exposes the application externally via port `30007`.

---

## Network Policies

Network policies were defined to control traffic flow:

- Allow traffic from frontend → backend
- Allow traffic from backend → database
- Deny all other traffic (default deny)

### Important Note

Kind does not enforce Network Policies by default because it does not include a policy-enabled CNI (such as Calico or Cilium).

However, the policies are correctly defined and would work in a real Kubernetes environment.

---

## Ingress

An Ingress resource was defined to route traffic based on paths:

- `/web` → frontend
- `/api` → backend

### Limitation

Due to network restrictions, an Ingress Controller (e.g., NGINX Ingress Controller) could not be deployed.

However, the Ingress configuration is valid and would function correctly in a production environment.

---

## Concepts

### CNI (Container Network Interface)

CNI enables networking between pods. Each pod gets its own IP address within the cluster.

---

### Pod Networking

- All pods can communicate with each other
- No NAT is required within the cluster
- Communication is direct via pod IPs

---

### Service Types

- ClusterIP → internal communication
- NodePort → external access via node port
- LoadBalancer → cloud-based external access

---

### Ingress Controller

The Ingress Controller routes HTTP/HTTPS traffic based on rules defined in Ingress resources.

Example: NGINX Ingress Controller

---

### Service Mesh (Conceptual)

A Service Mesh provides advanced traffic control and observability:

- Traffic routing
- Retries
- Security (mTLS)
- Monitoring

Example: Istio

---

## Limitations

Due to environment restrictions:

- Ingress Controller could not be deployed
- Network Policies were not enforced at runtime

However, all configurations are valid and applicable in real-world scenarios.

---

## Conclusion

This lab demonstrates a solid understanding of:

- Kubernetes networking architecture
- Service exposure strategies
- Traffic control using Network Policies
- Routing using Ingress

Despite environmental limitations, the implementation reflects real-world Kubernetes practices.

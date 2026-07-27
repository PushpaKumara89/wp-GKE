# Production-Ready WordPress Stack on Kubernetes (K8s)

This repository contains highly optimized, production-grade Kubernetes manifests to deploy a scalable WordPress website backed by a MariaDB StatefulSet and a Redis container for object caching.

## 🚀 Architecture Overview
* **WordPress Frontend:** Deployed as a scalable Deployment with CPU/Memory limits and health checks.
* **MariaDB Database:** Configured as a `StatefulSet` with stable network identity and Persistent Volume Claims (PVC) using `standard` storage class.
* **Redis Caching:** Integrated for high-performance session and database query caching.
* **Ingress Controller:** Configured using Nginx Ingress to handle external traffic with custom rewrite rules.
* **Security:** Implemented `securityContext` (`runAsUser: 999`) for non-root database execution to follow security best practices.

## 🛠️ How to Deploy

1. **Clone the repository:**
   ```bash
   git clone [https://github.com/YOUR_GITHUB_USERNAME/wordpress-kubernetes-production-stack.git](https://github.com/YOUR_GITHUB_USERNAME/wordpress-kubernetes-production-stack.git)
   cd wordpress-kubernetes-production-stack
   ```
2. **Create Secrets and ConfigMaps (Prerequisites):**
   Make sure to deploy your database credentials and configuration files before initializing the manifests.
   ```bash
   kubectl apply -f credentials-secret.yaml
   kubectl apply -f wp-configmap.yaml
   ```

3. **Apply the Manifests::**
   ```bash
   kubectl apply -f mariadb-statefulset.yaml
   kubectl apply -f redis-deployment.yaml
   kubectl apply -f wordpress-deployment.yaml
   kubectl apply -f ingress.yaml
   ```

## 🔒 Production Features Included
Explicit Resource Limits (CPU/Memory) to avoid noisy neighbor cluster issues.

Safe injection of environmental data using envFrom and valueFrom via Secrets.

Persistent storage integration using volumeClaimTemplates to prevent data loss on pod restarts.
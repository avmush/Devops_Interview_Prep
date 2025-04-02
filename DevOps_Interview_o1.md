# DevOps & Kubernetes Cheat Sheet + Common Interview Questions

This document combines:
1. **Cheat Sheet** – Simple, yet detailed summaries of essential topics (networking, Linux, Docker, Kubernetes, ArgoCD, security, etc.).
2. **Common Interview Questions** – Typical questions for each area to help you prepare for interviews.

---

## Table of Contents

1. [Cheat Sheet](#cheat-sheet)
   - [Networking Basics](#networking-basics)
   - [Linux Essentials](#linux-essentials)
   - [Docker & Containerization](#docker--containerization)
   - [Kubernetes Fundamentals](#kubernetes-fundamentals)
   - [Kubernetes Security & Admission](#kubernetes-security--admission)
   - [Monitoring & Logging](#monitoring--logging)
   - [ArgoCD & GitOps](#argocd--gitops)
   - [Security & Secrets Management](#security--secrets-management)
   - [Kubernetes Admin Commands](#kubernetes-admin-commands)
   - [Helm & Kustomize](#helm--kustomize)
   - [12-Factor App Methodology](#12-factor-app-methodology)
   - [Descriptor Files](#linux-file-descriptors)
   - [JSONPath vs. jq](#jsonpath-vs-jq)

2. [Common Interview Questions](#common-interview-questions)

---

# Cheat Sheet

Below are **key concepts** in DevOps & Kubernetes, simplified but still detailed enough for interviews or day-to-day reference.

---

## Networking Basics

- **Internal vs. Public IPs**  
  - **Internal (Private) IPs**: 10.x.x.x, 192.168.x.x, etc. These **cannot** be directly accessed from the internet.  
  - **Public IPs**: Assigned by your ISP, **globally routable** for internet traffic.

- **Subnet & CIDR**  
  - **CIDR Notation** (e.g., /24, /16) splits IP addresses into network vs. host.  
  - **/24** → up to 254 hosts, **/16** → thousands of hosts.

- **NAT (Network Address Translation)**  
  - **Private IP** machines use a **router** to translate traffic to a **public IP**.

- **DHCP**  
  - **Dynamic Host Configuration Protocol** automatically assigns IP addresses to devices from a pool.

- **Forward Proxy vs. Reverse Proxy**  
  - **Forward Proxy**: Clients → Proxy → Internet (common in corporate networks).  
  - **Reverse Proxy**: Internet → Proxy (e.g., NGINX) → internal servers.

- **Bastion Host**  
  - A **special server** for SSH into a private network. Only the **bastion** is exposed publicly, boosting security.

- **Firewall**  
  - **Filters network traffic** (inbound/outbound) based on rules; helps block malicious connections.

- **Load Average**  
  - **Represents** how many processes are running/waiting.  
  - **Compare** to number of CPU cores. If load avg <= CPU cores, system is not overloaded.

- **Overlay Networking & BGP**  
  - In Kubernetes, used to **connect pods** across nodes.  
  - Overlay (like VXLAN) or direct BGP routes for multi-cluster networks.

---

## Linux Essentials

- **Processes & States**  
  - **Running (R)**: actively on CPU  
  - **Sleeping (S)**: waiting for something (disk, network)  
  - **Zombie (Z)**: finished but not cleaned up by parent  
  - **Orphan**: parent died; adopted by init  
  - **Daemon**: background service (no terminal)

- **Context Switching**  
  - The kernel **pauses one process** and **resumes another** so multiple processes share the CPU quickly.

- **Swap & Virtual Memory**  
  - **Swap**: Uses disk as extra “RAM” (slower)  
  - **Virtual Memory**: Each process sees a large memory space, OS handles real memory behind the scenes.

- **File Descriptors**  
  - **Integers** referencing open files/sockets: 0=stdin,1=stdout,2=stderr,≥3=others.

- **Namespaces & cgroups**  
  - **Namespaces** isolate resources (PID, network, etc.) so containers/processes don’t see each other’s environment.  
  - **cgroups** limit CPU/memory usage for containers or processes.

- **Linux Filesystem & Inodes**  
  - **Inodes** store metadata (permissions, owner).  
  - Tools: `df` (disk space), `du` (directory usage), `lsof` (open files).

- **Boot Process**  
  1. **BIOS/UEFI** → hardware checks, finds boot device  
  2. **Bootloader (e.g. GRUB)** → loads OS kernel  
  3. **Kernel** → sets up drivers, memory management  
  4. **init/systemd** (PID 1) → starts system services  
  5. **Login** → user session

- **SSH & Port Forwarding**  
  - **SSH**: Secure shell, `ssh user@host` for remote.  
  - **Local Forwarding**: `ssh -L 8080:localhost:80 user@host`, a local port (8080) -> remote service (80).

---

## Docker & Containerization

- **Containers vs. VMs**  
  - **Containers**: Share host OS kernel → lighter, faster startup.  
  - **VMs**: Each has its own OS → heavier resource usage.

- **Dockerfile Essentials**  
  - **FROM**: base image  
  - **RUN**: commands at build time  
  - **CMD**: default command if none given  
  - **ENTRYPOINT**: main command that’s hard to override  
  - **EXPOSE**: documents container port (not a real firewall)

- **Multi-Stage Builds**  
  - Use **multiple `FROM`** lines:  
    - **Stage 1**: build/compile environment (big images like `golang`).  
    - **Stage 2**: minimal image (like `alpine`), only copy the final binary → smaller final image.

- **Docker vs. K8s Commands/Args**  
  - Docker `ENTRYPOINT` → K8s `command`  
  - Docker `CMD` → K8s `args`

- **Running Containers**  
  - `docker run -p 8080:80 image` → map container port 80 to host port 8080.

- **Other Runtimes**  
  - `runc`, `podman` → run containers without Docker daemon.

---

## Kubernetes Fundamentals

- **Core Objects**  
  - **Pod**: smallest deployable unit (1+ containers).  
  - **Deployment**: manages stateless pods, does rolling updates/rollbacks.  
  - **Service**: stable network endpoint (ClusterIP, NodePort, LoadBalancer).  
  - **ConfigMap/Secret**: store configuration (plain vs. sensitive).  
  - **Operators & CRDs**: extend K8s with new resource types & custom logic.

- **Storage**  
  - **PV (PersistentVolume)**: actual storage in cluster (e.g., local disk, cloud disk).  
  - **PVC (PersistentVolumeClaim)**: user request to use storage.  
  - **StorageClass**: defines how to provision volumes dynamically.  
  - **CSI**: standard plugin interface for storage providers.

- **Scaling & Autoscalers**  
  - **HPA (Horizontal Pod Autoscaler)**: adds/removes **pod replicas** (requires Metrics Server).  
  - **VPA (Vertical Pod Autoscaler)**: changes **CPU/memory requests** for pods (install separately).  
  - **Cluster Autoscaler**: adjusts node count in a cluster.

- **Static Pods**  
  - Managed by **kubelet** directly (not via API server).  
  - Commonly used for essential components like `etcd` or `kube-apiserver`.

- **Multi-Scheduler**  
  - You can deploy a **custom scheduler** alongside the default if you have special scheduling needs.

- **Kubeadm, GKE, kops, AKS**  
  - Tools for setting up clusters on-prem (kubeadm) or in the cloud (GKE for Google, kops for AWS, AKS for Azure).

- **Kubernetes DNS**  
  - Pod/Service addresses like `my-svc.my-namespace.svc.cluster.local`.

- **Scaling the Cluster Infrastructure**  
  - **Horizontal**: add more nodes (manually or via cluster autoscaler).  
  - **Vertical**: give nodes bigger machine types (less common approach).

- **Deployment Strategies**  
  - **Rolling Update** (default): gradually replace old pods with new.  
  - **Recreate**: shut down old pods completely, then start new pods.

- **Multi-Container & Init Containers**  
  - **Multi-container pods**: containers share network & volumes (e.g., main app + sidecar).  
  - **Init containers**: run first for setup tasks (like waiting for DB).

---

## Kubernetes Security & Admission

- **Authentication → Authorization (RBAC) → Admission**  
  1. **Authentication**: “Who are you?”  
  2. **RBAC**: Roles, RoleBindings, etc.  
  3. **Admission Controllers**: final checks/changes (validating/mutating) before creation.

- **Pod Security Standards (PSS) & Pod Security Admission (PSA)**  
  - Defines security levels: Privileged, Baseline, Restricted for pods.

- **Threat Modeling (STRIDE)**  
  - **S**poofing, **T**ampering, **R**epudiation, **I**nfo disclosure, **D**oS, **E**levation of privilege.  
  - Identify & prioritize cluster security risks.

- **Security Hardening Tips**  
  - Avoid public image repositories or ensure scanning.  
  - Run as non-root, enable SELinux/AppArmor.  
  - Restrict push/pull to image registries.  
  - Use network policies for traffic filtering.

- **TLS Certificates in Kubernetes**  
  - All components talk via TLS.  
  - `.crt/.pem` = public cert, `.key` = private key.  
  - Use K8s CA or external CA for CertificateSigningRequests (CSR).

---

## Monitoring & Logging

- **cAdvisor**  
  - Built into kubelet; collects container CPU/memory usage.  
  - Feeds data to Metrics Server (real-time only, no history).

- **Metrics Server**  
  - Needed for HPA, `kubectl top`.  
  - Doesn’t keep historical data (Prometheus does that).

- **Prometheus & Grafana**  
  - **Prometheus**: scrapes metrics, time-series DB.  
  - **Grafana**: visual dashboards and alerts.

- **Logging in Kubernetes**  
  - `kubectl logs -f pod [container]`.  
  - For centralized logs: Fluentd or Logstash → ES, Splunk, etc.

---

## ArgoCD & GitOps

- **ArgoCD Basics**  
  - A GitOps tool: your cluster syncs to a Git repo.  
  - `Application` CR: defines the Git source and target cluster/namespace.

- **Sync Strategies**  
  - **Manual**: you click a “Sync” button or run `argocd app sync`.  
  - **Auto-Sync**: ArgoCD watches Git and auto-applies changes.  
  - **Auto-Prune**: deletes resources removed from Git.  
  - **Self-Heal**: reverts any drift from the Git state if cluster changes occur.

- **Dex & Okta**  
  - **Dex**: OIDC identity broker for SSO in ArgoCD.  
  - **Okta**: external identity provider (SSO).  
  - Combined for secure, centralized user logins.

- **ArgoCD Vault Plugin**  
  - Retrieves secrets from HashiCorp Vault at deployment time.  
  - No plaintext secrets in Git.

---

## Security & Secrets Management

- **Sealed Secrets**  
  - Encrypt normal K8s secrets so they can be safely stored in Git.  
  - Cluster’s sealed secrets controller decrypts them at runtime.

- **HashiCorp Vault**  
  - A robust secrets manager, can generate dynamic credentials.  
  - Integrates with K8s or ArgoCD to supply secrets at runtime.

- **RBAC**  
  - **Role**: namespace-scoped perms, **ClusterRole**: cluster-wide.  
  - **RoleBinding** / **ClusterRoleBinding**: assign perms to users/groups.

- **Image Security**  
  - Scan images (CI/CD pipelines).  
  - Sign images and enforce only signed images.  
  - Don’t run containers as root; use approved base images.

---

## Kubernetes Admin Commands

- **Node Maintenance**  
  - `kubectl drain <node>`: evict pods so you can upgrade or stop that node.  
  - `kubectl cordon <node>`: mark node unschedulable (no new pods).  
  - `kubectl uncordon <node>`: allow scheduling again.

- **CertificateSigningRequest (CSR)**  
  - K8s can act as a CA and sign cert requests for your pods or services.

- **ServiceAccount**  
  - Assign to pods needing specific API rights; link with RBAC roles.

---

## Helm & Kustomize

- **Helm**  
  - A package manager for K8s (like apt for Linux).  
  - **Chart.yaml**, **values.yaml**, templates.  
  - **Releases**: each install is versioned in the cluster.

- **Kustomize**  
  - Built into `kubectl`.  
  - Allows **overlay** changes on top of base YAML.  
  - Great for environment-specific tweaks (dev, staging, prod).

---

## 12-Factor App Methodology

1. **Codebase** in version control  
2. **Dependencies** explicitly declared  
3. **Config** in environment variables  
4. **Backing services** treated like attached resources  
5. **Build, Release, Run** as separate stages  
6. **Stateless processes**  
7. **Port binding** (the app listens on a port)  
8. **Concurrency** (scale by running multiple processes)  
9. **Disposability** (fast startup/shutdown)  
10. **Dev/prod parity** (keep environments similar)  
11. **Logs** as event streams  
12. **Admin processes** run as one-offs

---

## Linux File Descriptors

A **file descriptor (FD)** in Linux is an integer that the operating system uses to identify an open file or I/O resource (like a socket or pipe). Here’s what you need to know:

1. **Integer Handles**  
   - FDs are simply small integers (`0`, `1`, `2`, …) used by the kernel to keep track of open resources.

2. **Standard File Descriptors**  
   - **0:** Standard Input (stdin)  
   - **1:** Standard Output (stdout)  
   - **2:** Standard Error (stderr)

3. **FDs ≥ 3**  
   - Assigned to additional opened files, sockets, or pipes.
   - The OS automatically picks the next available number whenever you open a new resource.

4. **Why They Matter**  
   - Provides a simple, uniform way to do I/O (read, write) across files, network sockets, etc.
   - Tools like `ls -l /proc/<PID>/fd` or `lsof` show which FDs a process is using.

5. **Closing FDs**  
   - When you close a file or when the process ends, the FD is released and can be reused for another resource.

**In summary**, file descriptors act as numeric “handles” to access files and other I/O in Linux, ensuring efficient resource management.


---

## JSONPath vs. jq

- **JSONPath** (built into `kubectl -o jsonpath`):
  - Quick extraction of fields.
  - Example:
    ```bash
    kubectl get nodes -o jsonpath='{.items[*].status.nodeInfo.osImage}'
    ```
- **jq** (external tool, advanced filtering):
  - Powerful JSON transformations.
  - Example:
    ```bash
    kubectl get nodes -o json | jq -r '.items[].status.nodeInfo.osImage'
    ```

---

# Common Interview Questions

Below are **commonly asked questions** for each area, to help you study or prepare.

## 1. Networking

1. **Explain private vs. public IP addresses.**  
2. **What is NAT and how does it work?**  
3. **How do subnet masks and CIDR work?**  
4. **Difference between forward proxy and reverse proxy?**  
5. **What is a bastion host and why use it?**

## 2. Linux Essentials

1. **What are zombie processes?** How do you handle them?  
2. **Explain the Linux boot process (BIOS → kernel).**  
3. **What are namespaces and cgroups used for?**  
4. **Swap space vs. RAM—why is swap slower?**  
5. **File descriptors—what are they and how are they used?**

## 3. Docker & Containerization

1. **How are containers different from VMs?**  
2. **Dockerfile instructions: FROM, RUN, CMD, ENTRYPOINT—explain each.**  
3. **What is a multi-stage build in Docker?**  
4. **How do you map container ports to the host?**  
5. **`ENTRYPOINT` vs. `CMD`—when would you use each?**

## 4. Kubernetes Fundamentals

1. **Explain Pods, Deployments, and Services.**  
2. **How does a Deployment handle rolling updates?**  
3. **What is a PVC (PersistentVolumeClaim)?**  
4. **Difference between NodePort and LoadBalancer Service?**  
5. **HPA vs. VPA—what do they each scale?**

## 5. Kubernetes Security & Admission

1. **What is RBAC and how do Roles/RoleBindings work?**  
2. **Validating vs. Mutating admission controllers—differences?**  
3. **What is the STRIDE model for threat modeling?**  
4. **Why avoid running containers as root?**  
5. **Explain Pod Security Standards (PSS) in simple terms.**

## 6. Monitoring & Logging

1. **What is cAdvisor and how does it relate to the Metrics Server?**  
2. **Explain Prometheus and Grafana—how do they work together?**  
3. **How do you view container logs in Kubernetes?**  
4. **Fluentd vs. Logstash—main differences?**  
5. **How do you check CPU/memory usage for pods or nodes in a cluster?**

## 7. ArgoCD & GitOps

1. **What is GitOps and how does ArgoCD implement it?**  
2. **Explain ArgoCD’s sync methods: auto, manual, pruning, self-heal.**  
3. **Dex vs. Okta—how do they integrate with ArgoCD?**  
4. **What does the ArgoCD Vault Plugin do?**  
5. **Explain ArgoCD’s Application CR—what fields are important?**

## 8. Security & Secrets Management

1. **What are Sealed Secrets and how do they differ from normal Secrets?**  
2. **How does HashiCorp Vault integrate with Kubernetes?**  
3. **How do Roles/RoleBindings tie to ServiceAccounts?**  
4. **What is image signing and why is it important?**  
5. **Why should we enable SELinux/AppArmor in container environments?**

## 9. Kubernetes Admin Commands

1. **What does `kubectl drain <node>` do?**  
2. **`kubectl cordon` vs. `kubectl uncordon`—when to use them?**  
3. **How do you handle TLS certificates (CSR) in Kubernetes?**  
4. **Describe rotating cluster certificates—why and how?**  
5. **How do ServiceAccounts relate to RBAC?**

## 10. Helm & Kustomize

1. **What is Helm and why use it?**  
2. **Difference between `Chart.yaml` and `values.yaml`?**  
3. **How do Helm releases track versions in the cluster?**  
4. **What is Kustomize and how does it compare to Helm?**  
5. **When to prefer Kustomize overlays over Helm charts?**

## 11. 12-Factor App Methodology

1. **What does ‘config in environment variables’ mean?**  
2. **Why should an app be stateless (factor 6)?**  
3. **Explain build, release, run stages.**  
4. **How do you treat logs as event streams?**  
5. **What is dev/prod parity and why is it important?**

## 12. Descriptor Files

1. **Examples of descriptor files (K8s YAML, Dockerfile, Terraform)?**  
2. **How do you define a Kubernetes Deployment in YAML?**  
3. **Difference between a Dockerfile and a Compose file?**  
4. **Why use Helm charts instead of raw YAML?**  
5. **Terraform vs. Helm—when do you use each?**

## 13. JSONPath vs. jq

1. **How do you extract a single field using JSONPath?**  
2. **What is `jq` good for beyond simple field extraction?**  
3. **When is JSONPath enough vs. when do you need `jq`?**  
4. **How do you filter JSON using `jq`?**  
5. **How do you pretty-print JSON with `jq`?**

---

# Final Thoughts

This **Mega Cheat Sheet** plus the **common interview questions** provide:
- **Simplified but detailed** explanations of DevOps and Kubernetes concepts.
- **Hands-on topics** like networking, Linux, containerization (Docker), and orchestrations (Kubernetes, ArgoCD).
- **Security highlights** (Sealed Secrets, Vault, RBAC, not running as root).
- **Monitoring/logging** approaches and tools (Prometheus, Fluentd).
- **Automation with Helm/Kustomize** for packaging K8s apps.
- **GitOps** approach with ArgoCD (auto-sync, self-heal, Dex/Okta integration).

Use this as a **study reference** or **interview prep**. Good luck, and happy DevOpsing!

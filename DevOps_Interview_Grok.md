# DevOps Cheat Sheet: Networking, Linux, Docker, Kubernetes, and More

## 1. Networking Basics
- **Internal vs. Public IPs**: Private (`10.x.x.x`, `192.168.x.x`) vs. Public (global). NAT translates private → public for internet.
- **Subnet & CIDR**: `/24` = 254 IPs, `/16` = 65,534 IPs.
- **DHCP**: Assigns IPs dynamically.
- **Bastion Host**: Secure jump box for SSH into private networks.
- **Firewall**: Filters traffic based on rules.
- **Load Average**: Processes in run/wait state (1, 5, 15 min). Compare to CPU cores.
- **Quorum in etcd**: Odd-numbered clusters (3, 5) for majority voting (K8s control plane).
- **Kubernetes Networking**:
  - **Built-In**: Pods get IPs, Services for stable IPs/names, Ingress for HTTP/HTTPS routing.
  - **Mandatory Add-Ons**:
    - **CNI Plugin (e.g., Flannel)**: Gives pods IPs, sets up network. Without it, pods cannot communicate (no IPs, no network).
      - Install: `kubectl apply -f https://raw.githubusercontent.com/flannel-io/flannel/master/Documentation/kube-flannel.yml`.
      - Verify: `kubectl get pods -n kube-system | grep flannel`.
    - **CoreDNS**: Resolves Service names (e.g., `hostname.namespace.svc.cluster.local` → IP). Without it, pods can’t find Services by name.
      - Install: `kubectl apply -f https://raw.githubusercontent.com/coredns/deployment/master/kubernetes/coredns.yaml`.
      - Verify: `kubectl get pods -n kube-system | grep coredns`.
  - **Overlay Networking**: Virtual network for pod-to-pod communication (e.g., Flannel uses VXLAN).
  - **BGP (Border Gateway Protocol)**: Advanced routing for K8s (e.g., Calico uses BGP for large-scale clusters).
- **Proxy & Firewall**:
  - Forward Proxy: Clients → Proxy → External.
  - Reverse Proxy: External → Proxy → Internal (e.g., Nginx for load balancing).
  - Firewall: Blocks/filters traffic.
- **Interview Questions**:
  - What’s the difference between private and public IPs? How does NAT work?
  - How does Kubernetes assign IPs to pods? What happens without a CNI plugin?
  - How does CoreDNS work in Kubernetes? What’s the DNS format for a Service?

## 2. Linux Essentials
- **Processes & States**: Running (R), Sleeping (S), Zombie (Z), Orphan, Daemon. Zombie: Finished, not reaped by parent.
- **Context Switching**: Kernel switches processes for multitasking.
- **Swap & Virtual Memory**: Swap extends RAM to disk (slower). Virtual memory: Each process sees its own space.
- **File Descriptors**: Numbers for open files/sockets: 0=stdin, 1=stdout, 2=stderr, ≥3=others. Check: `lsof -p <pid>`. Limits: `ulimit -n`.
- **Namespaces & cgroups**:
  - Namespaces: Isolate resources (PID, network, mount, IPC).
  - cgroups: Limit resource usage (CPU, memory).
- **Boot Process**: BIOS/UEFI → Bootloader (GRUB) → Kernel → init/systemd (PID 1) → Login.
- **SSH & Port Forwarding**:
  - SSH: `ssh user@host`. Key-based: `ssh-keygen`, `ssh-copy-id`.
  - Local Forwarding: `ssh -L 8080:localhost:80 user@remote_host`.
- **Linux Filesystem**:
  - Inodes: Metadata for files (e.g., permissions, size). Check: `df -i`.
  - Filesystem: Organizes data (e.g., ext4, xfs).
- **Linux Signals**: Messages to processes (e.g., `SIGTERM` to terminate, `SIGKILL` to force kill). Send: `kill -<signal> <pid>`.
- **Interview Questions**:
  - What’s a zombie process? How do you handle it?
  - How does context switching work in Linux?
  - What’s the difference between swap and virtual memory?

## 3. Docker & Containerization
- **Containers vs. VMs**: Containers share host OS kernel (light, fast). VMs have full guest OS (heavier).
- **Dockerfile**:
  - `FROM`: Base image.
  - `RUN`: Build-time commands.
  - `CMD`: Default command/args.
  - `ENTRYPOINT`: Main command.
  - `EXPOSE`: Documents ports.
- **Multi-Stage Builds**: Build stage (e.g., `golang`), final stage (e.g., `alpine`) → smaller image.
- **Docker vs. K8s Commands**: Docker `ENTRYPOINT` → K8s `command`, Docker `CMD` → K8s `args`.
- **Run Container**: `docker run -p hostPort:containerPort image`.
- **Other Runtimes**: `runc`, `podman` (no Docker daemon).
- **Interview Questions**:
  - What’s the difference between containers and VMs?
  - What’s the difference between `CMD` and `ENTRYPOINT` in a Dockerfile?
  - How do you reduce Docker image size?

## 4. Kubernetes Fundamentals
- **Core Objects**:
  - Pod: Smallest unit (1+ containers).
  - Deployment: Manages stateless pods.
  - Service: Stable endpoint (ClusterIP, NodePort, LoadBalancer).
  - ConfigMap/Secret: External config (plain vs. sensitive).
  - ServiceAccount: Identity for pods to access K8s API.
- **Storage**:
  - PV: Actual storage.
  - PVC: Storage request.
  - StorageClass: Dynamic provisioning.
  - CSI: Storage plugin standard.
- **Scaling**:
  - **Workloads**:
    - Horizontal: `kubectl scale` (manual), HPA (auto, e.g., `kubectl autoscale deploy my-app --cpu-percent=50 --min=1 --max=10`).
    - Vertical: `kubectl edit` (manual), VPA (auto, needs install).
  - **Cluster Infra**:
    - Horizontal: `kubectl join node` (manual), Cluster Autoscaler (auto).
    - Vertical: Not common.
- **Ingress vs. Gateway API**:
  - Ingress: HTTP/HTTPS routing (no UDP/TCP support).
  - Gateway API: Advanced routing (Gateway, GatewayClass, HTTPRoute/TCPRoute). Supports HTTP/2, WebSocket, TLS.
- **Operators & CRDs**:
  - CRD: Extends K8s API.
  - Operator: Custom controller for stateful apps (needs CRD).
- **Multi-Scheduler**: Add custom scheduler for specialized logic.
- **Admission Controllers**:
  - Pipeline: Authentication → Authorization → Admission → Creation.
  - Validating: Checks requests. Mutating: Modifies requests.
- **Static Pods**: Managed by kubelet (not API server). Used for critical components (e.g., apiserver, etcd).
- **cAdvisor**: Built into kubelet, collects container CPU/memory for Metrics Server.
- **Logging**: `kubectl logs -f pod-name`. Central: EFK/ELK.
- **Probes**:
  - Liveness: Checks if pod is alive (restarts if fails).
  - Readiness: Checks if pod is ready to serve traffic.
- **Node Management**:
  - `kubectl drain node-01`: Evict pods, make node unschedulable.
  - `kubectl cordon node-01`: Mark node unschedulable (no new pods).
  - `kubectl uncordon node-01`: Make node schedulable again.
- **TLS Certificates in K8s**:
  - All K8s components (e.g., kubelet, apiserver) use TLS for secure communication.
  - `.crt/.pem`: Public key. `.key/.key.pem`: Private key.
  - CA (Certificate Authority): Signs certificates in cluster.
  - Generate: Use `openssl` (e.g., `openssl genrsa -out my-key.key 2048`).
  - CertificateSigningRequest (CSR): Request K8s to sign a certificate.
- **K8s Cluster Setup**:
  - On-Prem: `kubeadm`.
  - Cloud: GKE (Google), AKS (Azure), EKS (AWS with `kops`).
  - etcd: Recommended on dedicated server. Leader manages writes.
- **Interview Questions**:
  - How does scaling work in Kubernetes? Difference between HPA and VPA?
  - What’s the difference between Ingress and Gateway API?
  - How do TLS certificates secure communication in Kubernetes?

## 5. Kubernetes Deployment & Rollouts
- **Rollout**: Updates create new revisions. Rollback: Revert to previous version.
- **Strategies**:
  - Recreate: Stop old, start new (downtime).
  - Rolling Update: Gradual replacement (zero downtime).
- **Multi-Container Pods**: Share network/volumes (e.g., sidecars).
- **InitContainers**: Run before main containers for setup (e.g., wait for DB).
- **Interview Questions**:
  - What’s the difference between Recreate and Rolling Update strategies?
  - When would you use an InitContainer?

## 6. ArgoCD & GitOps
- **ArgoCD Basics**: Syncs cluster with Git (GitOps).
- **Sync Types**:
  - Manual: `argocd app sync`.
  - Auto: Auto-deploys Git changes.
  - Auto-Prune: Removes resources not in Git.
  - Self-Heal: Reverts drift.
- **Dex & Okta**: Dex (SSO broker), Okta (identity provider).
- **ArgoCD Vault Plugin**: Pulls secrets from HashiCorp Vault.
- **Interview Questions**:
  - What is GitOps, and how does ArgoCD implement it?
  - What’s the difference between auto-sync and self-heal in ArgoCD?

## 7. Logging & Monitoring
- **EFK vs. ELK**:
  - EFK: Elasticsearch, Fluentd, Kibana (lightweight, K8s-friendly).
  - ELK: Elasticsearch, Logstash, Kibana (powerful pipelines).
  - Collects logs (e.g., “Error: DB failed”).
- **Fluentd vs. Logstash**:
  - Fluentd: Lightweight, K8s-friendly.
  - Logstash: More features, heavier.
- **Prometheus & Grafana**:
  - Prometheus: Scrapes metrics (e.g., CPU usage).
  - Grafana: Visualizes metrics.
  - Prometheus doesn’t check logs, only metrics.
- **Metrics Server**:
  - Enables HPA, `kubectl top`.
  - Install: `kubectl apply -f <metrics-server-url>`.
  - Collects CPU/memory from kubelets (via cAdvisor).
- **Interview Questions**:
  - What’s the difference between EFK and ELK?
  - How does Prometheus differ from EFK in monitoring?

## 8. Security & Secrets
- **Authentication & Authorization**:
  - **Authentication**: Verifies identity (“who are you?”) via tokens, certificates, or external providers (e.g., Okta).
  - **Authorization (RBAC)**:
    - Role/ClusterRole: Define permissions (e.g., “can read pods”).
    - RoleBinding/ClusterRoleBinding: Assign roles to users/service accounts.
  - **Admission Controllers**: Validate/modify requests after auth (e.g., Pod Security Admission).
- **Pod Security**:
  - **PSS (Pod Security Standards)**: Policies for pod security (e.g., no root, restricted ports).
  - **PSA (Pod Security Admission)**: Enforces PSS at admission (e.g., block non-compliant pods).
- **Threat Modeling**:
  - Identify security risks in K8s (e.g., exposed APIs, misconfigurations).
  - **STRIDE Model**:
    - Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege.
- **Image Security**:
  - Don’t use public image repos.
  - Scan images in CI/CD: Fail builds, quarantine if vulnerabilities found.
  - Sign/verify images cryptographically.
  - Policies: Use signed images, restrict push/pull, RBAC for repos, approved base images.
  - Scan IaC (e.g., Terraform) for misconfigurations.
- **Security Best Practices**:
  - Don’t run processes as root.
  - Enable SELinux for extra security.
  - Scan images for vulnerabilities.
- **Sealed Secrets**: Encrypt secrets for Git, decrypt in cluster.
- **HashiCorp Vault**: Central secrets manager, dynamic secrets.
- **securityContext**:
  - Add capabilities (e.g., `capabilities: add: ["SYS_TIME"]` for time changes).
- **Interview Questions**:
  - What’s the difference between authentication and authorization in Kubernetes?
  - How does RBAC work in Kubernetes?
  - What are some best practices for securing container images?

## 9. Nginx & Reverse Proxy
- **Nginx**: Web server, reverse proxy, load balancer, K8s Ingress Controller.
- **Forward vs. Reverse Proxy**:
  - Forward: Clients → Proxy → External.
  - Reverse: External → Proxy → Internal.
- **Interview Questions**:
  - What’s the difference between a forward and reverse proxy?
  - How does Nginx work as an Ingress Controller in Kubernetes?

## 10. 12-Factor App Methodology
- Codebase: Version control.
- Dependencies: Declare explicitly.
- Config: Env variables.
- Backing Services: Attached resources.
- Build, Release, Run: Separate stages.
- Stateless: No local state.
- Port Binding: Export services via ports.
- Concurrency: Scale out.
- Disposability: Quick start/stop.
- Dev/Prod Parity: Keep similar.
- Logs: Event streams.
- Admin Processes: One-offs.
- **Interview Questions**:
  - What are the key principles of the 12-Factor App methodology?
  - How do you handle configuration in a 12-Factor app?

## 11. Descriptor Files & Tools
- **Kubernetes YAML**: Deployments, Services, Ingress, etc.
- **Dockerfile**: Build images.
- **Helm**:
  - Package manager for K8s.
  - Components: Helm CLI, charts, releases (tracks revisions), templates, `Chart.yaml` (chart info), `values.yaml` (config).
  - Artifact Hub: `artifacthub.io` for charts.
- **Kustomize**:
  - Built into `kubectl`.
  - `kustomization.yaml`: Define resources, apply patches/overlays.
  - Base: Common config. Overlays: Environment-specific changes.
- **Terraform**: `.tf` files for infrastructure as code.
- **JSONPath vs. jq**:
  - JSONPath: `kubectl -o jsonpath` (quick extraction).
  - jq: `kubectl get nodes -o json | jq ...` (powerful querying).
- **Interview Questions**:
  - What’s the difference between Helm and Kustomize?
  - How do you use JSONPath to query Kubernetes resources?

## 12. Managed vs. On-Prem Kubernetes
- **Managed Clusters**:
  - GKE (Google), AKS (Azure), EKS (AWS with `kops`).
  - Control plane managed by provider.
- **On-Prem**: `kubeadm` for self-managed clusters.
- **etcd**: Dedicated server recommended. Leader manages writes.
- **Interview Questions**:
  - What’s the difference between a managed and on-prem Kubernetes cluster?
  - Why is etcd recommended on a dedicated server?

## How to Use This Cheat Sheet
- **For Learning**: Quick reference for key concepts (e.g., Flannel, CoreDNS, RBAC).
- **For Troubleshooting**: Commands (e.g., `kubectl get pods -o wide`, `kubectl drain`).
- **For Interviews**: Prepare with common questions (e.g., RBAC, scaling, security).

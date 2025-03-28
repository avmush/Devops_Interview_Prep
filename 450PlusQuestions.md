# Part 1: Linux, Docker, Kubernetes
## Linux (30 Questions)

### Process Management
**Q:** How do you check the current running processes?  
**A:** Use `top` or `htop` for an interactive view, or `ps aux` for a detailed list.  

**Q:** How do you kill a process by PID?  
**A:** Use `kill -9 <PID>` for a forceful termination.  

**Q:** What is the `/proc` directory?  
**A:** A virtual filesystem providing process and system information.  

---

### File System & Permissions
**Q:** How do you change a file’s ownership?  
**A:** Use `chown <user>:<group> <file>` (e.g., `chown john:dev file.txt`).  

**Q:** What does `chmod 755` mean?  
**A:** Sets read/write/execute for owner, read/execute for group and others.  

**Q:** What is a symbolic link?  
**A:** A file that points to another file/directory, created with `ln -s`.  

**Q:** How do you find a file by name?  
**A:** Use `find / -name "filename"` or `locate filename` (faster, requires `updatedb`).  

---

### Disk & Storage
**Q:** What does the `df -h` command do?  
**A:** Displays disk space usage in a human-readable format.  

**Q:** How do you check disk I/O?  
**A:** Use `iostat` or `vmstat` to monitor disk performance.  

**Q:** What does `lsblk` do?  
**A:** Lists block devices (e.g., disks and partitions).  

**Q:** How do you mount a filesystem?  
**A:** Use `mount /dev/sdX /mnt/point` (check `/etc/fstab` for persistence).  

---

### Networking
**Q:** How do you check network connectivity?  
**A:** Use `ping <ip>` or `curl <url>` to test connectivity.  

**Q:** How do you list open ports?  
**A:** Use `netstat -tuln` or `ss -tuln`.  

**Q:** What is the purpose of `/etc/hosts`?  
**A:** Maps hostnames to IP addresses for local DNS resolution.  

---

### Text Processing
**Q:** What does `grep` do?  
**A:** Searches text for patterns (e.g., `grep "error" log.txt`).  

**Q:** What is the `awk` command?  
**A:** A text-processing tool for pattern matching and data extraction.  

**Q:** What is the `tail` command?  
**A:** Displays the last few lines of a file (e.g., `tail -n 10 file.txt`).  

---

### System Info & Logs
**Q:** What is the `uname` command?  
**A:** Displays system information (e.g., `uname -r` for kernel version).  

**Q:** What is the `uptime` command?  
**A:** Shows how long the system has been running.  

**Q:** How do you check system logs?  
**A:** Use `journalctl` or view files in `/var/log` (e.g., `/var/log/syslog`).  

---

### Shell & Scripting
**Q:** What is a shell script?  
**A:** A file with executable commands, typically starting with `#!/bin/bash`.  

**Q:** How do you redirect output to a file?  
**A:** Use `>` (overwrite) or `>>` (append), e.g., `ls > output.txt`.  

**Q:** How do you set an environment variable?  
**A:** Use `export VAR=value` (e.g., `export PATH=$PATH:/usr/local/bin`).  

---

### Compression & Sync
**Q:** How do you compress a file?  
**A:** Use `tar -czvf archive.tar.gz <file>` for gzip compression.  

**Q:** What is `rsync` used for?  
**A:** Synchronizes files between directories or systems efficiently.  

---

### Scheduling & Users
**Q:** How do you schedule a task in Linux?  
**A:** Use `cron` with `crontab -e` to edit scheduled jobs.  

**Q:** What is the `whoami` command?  
**A:** Displays the current user’s username.  

**Q:** What does `sudo` do?  
**A:** Runs a command as a superuser or another user.  



## Docker (30 Questions)

### Basics
**Q:** What is Docker?  
**A:** A platform for containerizing applications, ensuring consistency across environments.  

**Q:** What is the difference between an image and a container?  
**A:** An image is a static template; a container is a running instance of an image.  

**Q:** What is a Dockerfile?  
**A:** A script with instructions to build a Docker image.  

### Container Management
**Q:** How do you list all running containers?  
**A:** Use `docker ps` (add `-a` for all containers).  

**Q:** How do you run a container in detached mode?  
**A:** Use `docker run -d <image-name>`.  

**Q:** How do you stop a running container?  
**A:** Use `docker stop <container-id>`.  

**Q:** How do you restart a container?  
**A:** Use `docker restart <container-id>`.  

**Q:** How do you remove a container?  
**A:** Use `docker rm <container-id>` (must be stopped first).  

**Q:** What is the difference between `docker stop` and `docker kill`?  
**A:** `stop` gracefully stops; `kill` forcefully terminates.  

### Images
**Q:** How do you pull an image from Docker Hub?  
**A:** Use `docker pull <image-name>:<tag>` (e.g., `docker pull nginx:latest`).  

**Q:** How do you build an image?  
**A:** Use `docker build -t <image-name>:<tag> .` in a directory with a Dockerfile.  

**Q:** How do you list all images?  
**A:** Use `docker images`.  

**Q:** How do you remove an image?  
**A:** Use `docker rmi <image-id>`.  

**Q:** How do you tag an image?  
**A:** Use `docker tag <source-image> <new-name>:<tag>`.  

### Networking & Volumes
**Q:** How do you map a port in Docker?  
**A:** Use `-p <host-port>:<container-port>` (e.g., `docker run -p 80:80 nginx`).  

**Q:** What is a Docker network?  
**A:** A communication channel between containers, created with `docker network create`.  

**Q:** What is a Docker volume?  
**A:** Persistent storage for containers, managed with `docker volume create`.  

**Q:** What is a bind mount?  
**A:** Maps a host directory into a container (e.g., `-v /host:/container`).  

### Dockerfile Instructions
**Q:** What is the `ENTRYPOINT` in a Dockerfile?  
**A:** Specifies the default executable for a container.  

**Q:** What is the `CMD` instruction?  
**A:** Provides default arguments for an `ENTRYPOINT` or runs a command in a container.  

**Q:** What is the `EXPOSE` instruction?  
**A:** Documents ports an image intends to use, but doesn’t publish them.  

**Q:** What is a multi-stage build?  
**A:** Uses multiple `FROM` statements to optimize image size.  

### Advanced Features
**Q:** What does `docker-compose` do?  
**A:** Manages multi-container applications defined in a YAML file.  

**Q:** What is a Docker registry?  
**A:** A storage system for Docker images (e.g., Docker Hub).  

**Q:** What is Docker Swarm?  
**A:** A native orchestration tool for managing Docker containers.  

**Q:** How do you inspect a container?  
**A:** Use `docker inspect <container-id>` for detailed metadata.  

### Debugging & Maintenance
**Q:** How do you check Docker logs?  
**A:** Use `docker logs <container-id>`.  

**Q:** How do you run a command in a running container?  
**A:** Use `docker exec -it <container-id> <command>` (e.g., `bash`).  

**Q:** How do you prune unused Docker objects?  
**A:** Use `docker system prune`.  

**Q:** How do you check Docker version?  
**A:** Use `docker --version`.  

---

## Kubernetes (30 Questions)

### Basics
**Q:** What is Kubernetes?  
**A:** An open-source platform for automating deployment, scaling, and management of containerized applications.  

**Q:** What is a Pod?  
**A:** The smallest deployable unit in Kubernetes, containing one or more containers.  

**Q:** What is a Namespace?  
**A:** A way to partition resources within a cluster for isolation.  

### Workloads
**Q:** How do you create a deployment?  
**A:** Use `kubectl create deployment <name> --image=<image>`.  

**Q:** What is a ReplicaSet?  
**A:** Ensures a specified number of Pod replicas are running at all times.  

**Q:** How do you scale a deployment?  
**A:** Use `kubectl scale deployment <name> --replicas=<number>`.  

**Q:** What is a StatefulSet?  
**A:** Manages stateful applications with persistent identities.  

**Q:** What is a DaemonSet?  
**A:** Ensures a Pod runs on every node in the cluster.  

**Q:** What is a Job?  
**A:** Runs a task to completion, creating one or more Pods.  

**Q:** What is a CronJob?  
**A:** Schedules Jobs to run at specific times.  

### Services & Networking
**Q:** What is a Kubernetes Service?  
**A:** An abstraction providing a stable IP and DNS name for accessing Pods.  

**Q:** How do you expose a deployment?  
**A:** Use `kubectl expose deployment <name> --port=<port> --type=<type>`.  

**Q:** What is a NodePort Service?  
**A:** Exposes a Service on a specific port of each node.  

**Q:** What is an Ingress?  
**A:** Manages external HTTP/HTTPS traffic to Services.  

### Storage
**Q:** What is a PersistentVolume (PV)?  
**A:** A cluster-wide storage resource provisioned by an admin.  

**Q:** What is a PersistentVolumeClaim (PVC)?  
**A:** A request for storage by a user, bound to a PV.  

### Configuration
**Q:** What is a ConfigMap?  
**A:** Stores configuration data as key-value pairs for Pods.  

**Q:** What is a Secret?  
**A:** Stores sensitive data like passwords, encoded in base64.  

### Cluster Management
**Q:** How do you check cluster nodes?  
**A:** Use `kubectl get nodes`.  

**Q:** What is the role of `kube-scheduler`?  
**A:** Assigns Pods to nodes based on resource availability.  

**Q:** What is the Kubernetes API server?  
**A:** The central management component exposing the Kubernetes API.  

**Q:** What is `kubelet`?  
**A:** An agent running on each node to manage Pods.  

**Q:** What is the role of `etcd`?  
**A:** A distributed key-value store for cluster configuration data.  

### Scaling & Updates
**Q:** How do you update a deployment?  
**A:** Use `kubectl set image deployment/<name> <container>=<new-image>`.  

**Q:** What is a HorizontalPodAutoscaler (HPA)?  
**A:** Scales Pods based on CPU/memory usage.  

### RBAC & Security
**Q:** What is a ClusterRole?  
**A:** Defines permissions across the entire cluster.  

**Q:** How do you taint a node?  
**A:** Use `kubectl taint nodes <node-name> key=value:NoSchedule`.  

### Debugging
**Q:** How do you check Pod logs?  
**A:** Use `kubectl logs <pod-name>`.  

**Q:** How do you describe a resource?  
**A:** Use `kubectl describe <resource> <name>` (e.g., `kubectl describe pod my-pod`).  

**Q:** How do you delete a Pod?  
**A:** Use `kubectl delete pod <pod-name>`.

# Part 2: Networking, CI/CD, ArgoCD, AWS

## Networking (30 Questions)

### Fundamentals
**Q:** What is an IP address?  
**A:** A unique identifier for a device on a network (e.g., `192.168.1.1`).  

**Q:** What is the difference between TCP and UDP?  
**A:** TCP is connection-oriented and reliable; UDP is connectionless and faster.  

**Q:** What is DNS?  
**A:** Domain Name System translates domain names (e.g., `google.com`) to IP addresses.  

**Q:** What is a subnet mask?  
**A:** Defines the network portion of an IP address (e.g., `255.255.255.0`).  

### Protocols & Tools
**Q:** How do you check open ports on a system?  
**A:** Use `netstat -tuln` or `ss -tuln`.  

**Q:** How does `ping` work?  
**A:** Sends ICMP echo requests to test connectivity to a host.  

**Q:** What is ARP?  
**A:** Address Resolution Protocol maps IPs to MAC addresses.  

**Q:** How do you traceroute a network path?  
**A:** Use `traceroute <host>` or `tracert` (Windows) to see the route.  

### Security
**Q:** What is a firewall?  
**A:** A security system that controls network traffic based on rules.  

**Q:** What is an SSL certificate?  
**A:** Secures data transmission with encryption (HTTPS).  

**Q:** What is a VPN?  
**A:** Virtual Private Network encrypts traffic over public networks.  

**Q:** How do you configure a firewall rule?  
**A:** Use `iptables` or `ufw` (e.g., `ufw allow 22`).  

### Advanced Concepts
**Q:** What is a VLAN?  
**A:** A virtual LAN that segments a network logically without additional hardware.  

**Q:** What is NAT?  
**A:** Network Address Translation maps private IPs to a public IP.  

**Q:** What is BGP?  
**A:** Border Gateway Protocol routes traffic between autonomous systems.  

**Q:** What is a CDN?  
**A:** Content Delivery Network distributes content closer to users.  

### Infrastructure
**Q:** What is a load balancer?  
**A:** Distributes network traffic across multiple servers for reliability.  

**Q:** What is the purpose of a gateway?  
**A:** Routes traffic between networks (e.g., to the internet).  

**Q:** What is a proxy server?  
**A:** Acts as an intermediary between clients and servers.  

**Q:** What is DHCP?  
**A:** Dynamic Host Configuration Protocol assigns IPs automatically.  

### Technical Details
**Q:** What is the OSI model?  
**A:** A 7-layer framework for network communication (Physical to Application).  

**Q:** What is a MAC address?  
**A:** A unique hardware identifier for network devices.  

**Q:** What is a socket?  
**A:** An endpoint for communication (IP + port).  

**Q:** What is a packet?  
**A:** A unit of data transmitted over a network.  

### IPv6 & Performance
**Q:** What is the difference between IPv4 and IPv6?  
**A:** IPv4 uses 32 bits (e.g., `192.168.1.1`); IPv6 uses 128 bits (e.g., `2001:db8::1`).  

**Q:** How do you test network speed?  
**A:** Use `iperf` or `speedtest-cli`.  

**Q:** What is latency?  
**A:** The delay in data transmission over a network.  

### Ports & Interfaces
**Q:** What is port 80 used for?  
**A:** HTTP traffic (web browsing).  

**Q:** How do you check network interfaces?  
**A:** Use `ifconfig` or `ip addr`.  

**Q:** How do you set a static IP?  
**A:** Edit network config files (e.g., `/etc/network/interfaces`).  

---

## CI/CD (30 Questions)

### Core Concepts
**Q:** What is CI/CD?  
**A:** Continuous Integration/Continuous Deployment automates building, testing, and deploying code.  

**Q:** What is a pipeline?  
**A:** A series of automated steps in a CI/CD process.  

**Q:** What is continuous integration?  
**A:** Frequently merging code changes with automated testing.  

### Tools
**Q:** What is Jenkins?  
**A:** An open-source CI/CD tool with extensive plugin support.  

**Q:** What is TeamCity?  
**A:** A CI/CD server with a user-friendly UI and build chaining.  

**Q:** What is GitLab CI?  
**A:** A built-in CI/CD system in GitLab using `.gitlab-ci.yml`.  

### Deployment Strategies
**Q:** What is blue-green deployment?  
**A:** Runs two identical environments, switching traffic to the new one.  

**Q:** What is a canary deployment?  
**A:** Rolls out changes to a small subset of users first.  

**Q:** What is a rollback in CI/CD?  
**A:** Reverts to a previous stable version if deployment fails.  

### Pipeline Components
**Q:** What is a build agent?  
**A:** A server or container executing CI/CD tasks.  

**Q:** What is a deployment artifact?  
**A:** A compiled or packaged output (e.g., `.jar`, `.war`).  

**Q:** What is a test suite?  
**A:** A collection of automated tests run in CI.  

### Integration & Triggers
**Q:** How does Git integrate with CI/CD?  
**A:** Acts as the source of truth for code and pipeline configs.  

**Q:** What is a webhook?  
**A:** An HTTP callback notifying a CI system of code changes.  

**Q:** What is a build trigger?  
**A:** An event starting a pipeline (e.g., commit).  

### Security & Optimization
**Q:** How do you secure a pipeline?  
**A:** Use secrets management (e.g., Vault) and restrict access.  

**Q:** What is a build cache?  
**A:** Speeds up builds by reusing previous results.  

**Q:** How do you parallelize a pipeline?  
**A:** Run independent steps simultaneously (e.g., in Jenkins).  

### Advanced Features
**Q:** What is a matrix build?  
**A:** Tests across multiple configurations (e.g., OS versions).  

**Q:** What is a post-deploy step?  
**A:** Actions after deployment (e.g., smoke tests).  

**Q:** What is a pull request build?  
**A:** Validates code changes before merging.  

### Monitoring & Debugging
**Q:** How do you monitor a pipeline?  
**A:** Use dashboards or logs in tools like Jenkins or TeamCity.  

**Q:** How do you handle pipeline failures?  
**A:** Set notifications and rollback mechanisms.  

**Q:** What is a deployment script?  
**A:** Automates deployment steps (e.g., Bash, Python).  

### Docker & Environments
**Q:** What is Docker in CI/CD?  
**A:** Provides consistent environments for building and testing.  

**Q:** What is a deployment environment?  
**A:** A target like `dev`, `staging`, or `prod`.  

**Q:** What is a release pipeline?  
**A:** Manages the delivery of a production-ready build.  

### Extensibility
**Q:** What is a CI/CD plugin?  
**A:** Extends tool functionality (e.g., Git plugin in Jenkins).  

**Q:** What is a pipeline variable?  
**A:** A configurable value used in pipeline steps.  

**Q:** How do you trigger a pipeline?  
**A:** By a code commit, schedule, or manual trigger.  

---

## ArgoCD (20 Questions)

### Basics
**Q:** What is ArgoCD?  
**A:** A declarative, GitOps-based continuous delivery tool for Kubernetes.  

**Q:** What is GitOps?  
**A:** A methodology where Git is the source of truth for deployments.  

**Q:** How does ArgoCD sync applications?  
**A:** Compares Git repo state with the cluster and applies changes.  

### Installation & Setup
**Q:** How do you install ArgoCD?  
**A:** Use `kubectl apply -n argocd -f <install-manifest>`.  

**Q:** How do you log in to ArgoCD UI?  
**A:** Use `argocd admin initial-password` for the initial password.  

**Q:** How do you add a Git repo?  
**A:** Use `argocd repo add <repo-url> --username <user>`.  

### Application Management
**Q:** What is an Application in ArgoCD?  
**A:** A Kubernetes resource managed by ArgoCD, defined in Git.  

**Q:** What is a sync policy?  
**A:** Defines how ArgoCD applies changes (e.g., auto-sync).  

**Q:** What is a health check?  
**A:** Assesses resource health (e.g., Pod readiness).  

### Operations
**Q:** How do you rollback an app?  
**A:** Use `argocd app rollback <app-name> <revision>`.  

**Q:** How do you check app status?  
**A:** Use `argocd app get <app-name>`.  

**Q:** How do you delete an app?  
**A:** Use `argocd app delete <app-name>`.  

### Advanced Features
**Q:** What is an ApplicationSet?  
**A:** Automates creating multiple Applications from a template.  

**Q:** What is a sync wave?  
**A:** Controls the order of resource application during sync.  

**Q:** What is a prune operation?  
**A:** Removes resources not in Git during sync.  

### Security & RBAC
**Q:** How do you configure RBAC?  
**A:** Edit `argocd-rbac-cm` ConfigMap with policies.  

**Q:** What is a managed namespace?  
**A:** The namespace where ArgoCD deploys resources.  

**Q:** What are notifications in ArgoCD?  
**A:** Alerts (e.g., Slack) for application events.  

### CLI & Automation
**Q:** What is the ArgoCD CLI?  
**A:** A tool to manage ArgoCD (e.g., `argocd app sync`).  

**Q:** How do you enable auto-sync?  
**A:** Set `syncPolicy: automated` in the Application manifest.  

---

## AWS (30 Questions)

### Core Services
**Q:** What is AWS?  
**A:** Amazon Web Services, a cloud platform offering compute, storage, and more.  

**Q:** What is an EC2 instance?  
**A:** A virtual server in AWS for running applications.  

**Q:** What is S3?  
**A:** Simple Storage Service, an object storage system.  

### Compute & Storage
**Q:** What is Lambda?  
**A:** Serverless compute executing code in response to events.  

**Q:** What is EBS?  
**A:** Elastic Block Store, persistent storage for EC2.  

**Q:** What is ECS?  
**A:** Elastic Container Service for running Docker containers.  

### Networking
**Q:** What is a VPC?  
**A:** Virtual Private Cloud, an isolated network in AWS.  

**Q:** What is an ELB?  
**A:** Elastic Load Balancer distributes traffic across instances.  

**Q:** What is a NAT Gateway?  
**A:** Allows private subnets to access the internet.  

### Databases
**Q:** What is RDS?  
**A:** Relational Database Service for managed databases.  

**Q:** What is DynamoDB?  
**A:** A managed NoSQL database service.  

### Security & IAM
**Q:** What is IAM?  
**A:** Identity and Access Management controls permissions.  

**Q:** How do you secure an S3 bucket?  
**A:** Use bucket policies and IAM roles to restrict access.  

**Q:** What is a Security Group?  
**A:** A virtual firewall for EC2 instances.  

### Management Tools
**Q:** What is CloudWatch?  
**A:** Monitors AWS resources and applications.  

**Q:** What is CloudFormation?  
**A:** Infrastructure-as-Code (IaC) to provision AWS resources.  

**Q:** What is the AWS CLI?  
**A:** A command-line tool to manage AWS services.  

### Deployment & Scaling
**Q:** What is Auto Scaling?  
**A:** Adjusts EC2 capacity based on demand.  

**Q:** What is EKS?  
**A:** Elastic Kubernetes Service for managed Kubernetes.  

**Q:** What is Fargate?  
**A:** A serverless compute engine for containers.  

### DNS & Messaging
**Q:** What is Route 53?  
**A:** A scalable DNS and domain registration service.  

**Q:** What is SNS?  
**A:** Simple Notification Service for sending messages.  

**Q:** What is SQS?  
**A:** Simple Queue Service for message queuing.  

### Technical Details
**Q:** What is an AMI?  
**A:** Amazon Machine Image, a template for EC2 instances.  

**Q:** How do you launch an EC2 instance?  
**A:** Use the AWS Console, CLI, or SDK with an AMI and instance type.  

**Q:** How do you create a subnet?  
**A:** Define it within a VPC in the AWS Console or CLI.  

### Regions & Availability
**Q:** What is a region in AWS?  
**A:** A geographic area with multiple data centers.  

**Q:** What is an availability zone?  
**A:** An isolated location within a region.  

**Q:** How do you SSH into an EC2 instance?  
**A:** Use `ssh -i <key.pem> <user>@<ip>`.  

### Encryption
**Q:** How do you encrypt data in S3?  
**A:** Enable server-side encryption (SSE) with AES-256.  

# Part 3: GCP, Terraform, Ansible, Prometheus & Grafana

## GCP (30 Questions)

### Core Services
**Q:** What is Google Cloud Platform (GCP)?  
**A:** A suite of cloud services by Google for compute, storage, and more.  

**Q:** What is a Compute Engine?  
**A:** GCP's virtual machine service, similar to AWS EC2.  

**Q:** What is Cloud Storage?  
**A:** Object storage for unstructured data, like AWS S3.  

### Compute & Serverless
**Q:** What is Cloud Functions?  
**A:** Serverless compute for event-driven code, like AWS Lambda.  

**Q:** What is GKE?  
**A:** Google Kubernetes Engine, managed Kubernetes service.  

**Q:** What is Cloud Run?  
**A:** A serverless platform for containerized apps.  

### Networking
**Q:** What is a VPC in GCP?  
**A:** Virtual Private Cloud, a logically isolated network.  

**Q:** What is Cloud Load Balancing?  
**A:** Distributes traffic across instances globally.  

**Q:** What is VPC Network Peering?  
**A:** Connects two VPCs for private communication.  

### Storage & Databases
**Q:** What is Persistent Disk?  
**A:** Block storage for Compute Engine VMs.  

**Q:** What is Cloud SQL?  
**A:** A managed relational database service.  

**Q:** What is Datastore?  
**A:** A NoSQL database for scalable apps.  

### Security & IAM
**Q:** What is IAM in GCP?  
**A:** Identity and Access Management controls permissions.  

**Q:** How do you secure Cloud Storage?  
**A:** Use IAM policies and bucket-level permissions.  

**Q:** How do you encrypt data in Cloud Storage?  
**A:** Enable server-side encryption (default) or use customer-managed keys.  

### Management Tools
**Q:** What is Cloud Monitoring?  
**A:** Tracks performance metrics of GCP resources.  

**Q:** What is Deployment Manager?  
**A:** Infrastructure-as-code tool for GCP resources.  

**Q:** What is the `gcloud` CLI?  
**A:** A command-line tool for managing GCP resources.  

### Data & Analytics
**Q:** What is BigQuery?  
**A:** A serverless data warehouse for analytics.  

**Q:** What is Pub/Sub?  
**A:** A messaging service for event-driven systems.  

### Operations
**Q:** How do you launch a VM in GCP?  
**A:** Use the GCP Console or `gcloud compute instances create`.  

**Q:** How do you create a subnet in GCP?  
**A:** Define it within a VPC using the Console or CLI.  

**Q:** How do you SSH into a VM?  
**A:** Use `gcloud compute ssh <instance-name>`.  

### Scaling & Configuration
**Q:** What is Auto Scaling in GCP?  
**A:** Adjusts instance groups based on load, via Managed Instance Groups.  

**Q:** What is a machine type?  
**A:** A predefined or custom VM configuration (e.g., `n1-standard-2`).  

### DNS & Hybrid Cloud
**Q:** What is Cloud DNS?  
**A:** A managed DNS service for domain resolution.  

**Q:** What is Anthos?  
**A:** A hybrid/multi-cloud management platform.  

### Firewall & Regions
**Q:** What are Firewall Rules?  
**A:** Network rules controlling traffic to VMs.  

**Q:** What is a region in GCP?  
**A:** A geographic area with multiple zones.  

**Q:** What is a zone?  
**A:** An isolated location within a region.  

---

## Terraform (30 Questions)

### Basics
**Q:** What is Terraform?  
**A:** An open-source tool for infrastructure as code (IaC).  

**Q:** What is HCL?  
**A:** HashiCorp Configuration Language, used by Terraform.  

### Providers & Resources
**Q:** What is a provider in Terraform?  
**A:** A plugin defining resources (e.g., AWS, GCP).  

**Q:** What is a resource in Terraform?  
**A:** A component of infrastructure (e.g., an EC2 instance).  

**Q:** How do you specify a provider version?  
**A:** Use `required_providers` block with version constraints.  

### State Management
**Q:** What is a Terraform state file?  
**A:** Tracks the current state of managed infrastructure.  

**Q:** How do you manage state remotely?  
**A:** Use a backend like S3 or Terraform Cloud.  

**Q:** What is `terraform show`?  
**A:** Displays the current state or plan.  

### Execution
**Q:** How do you initialize a Terraform project?  
**A:** Run `terraform init` to download providers.  

**Q:** How do you plan changes?  
**A:** Use `terraform plan` to preview changes.  

**Q:** How do you apply changes?  
**A:** Use `terraform apply` to create/update resources.  

### Modules & Reusability
**Q:** What is a module?  
**A:** A reusable set of Terraform configurations.  

**Q:** How do you import existing resources?  
**A:** Use `terraform import <resource> <id>`.  

### Variables & Outputs
**Q:** What is a variable in Terraform?  
**A:** A parameter for customizing configurations.  

**Q:** How do you define a variable?  
**A:** Use `variable "name" { default = "value" }`.  

**Q:** What is an output?  
**A:** A value returned after applying (e.g., an IP address).  

### Advanced Features
**Q:** What is a data source?  
**A:** Fetches existing resource data (e.g., AMI IDs).  

**Q:** What is a provisioner?  
**A:** Executes scripts on resources during creation.  

**Q:** What is `terraform taint`?  
**A:** Marks a resource for recreation on next apply.  

### Workspaces & Environments
**Q:** What is a workspace?  
**A:** Manages multiple environments (e.g., dev, prod).  

**Q:** How do you switch workspaces?  
**A:** Use `terraform workspace select <name>`.  

### Loops & Conditionals
**Q:** What is a `count` in Terraform?  
**A:** Creates multiple instances of a resource.  

**Q:** What is a `for_each` loop?  
**A:** Creates resources from a map or set.  

### Debugging & Validation
**Q:** How do you debug Terraform?  
**A:** Use `TF_LOG=DEBUG` environment variable.  

**Q:** What is `terraform validate`?  
**A:** Checks syntax and configuration validity.  

**Q:** What is `terraform fmt`?  
**A:** Formats Terraform files for consistency.  

### Dependencies & Locking
**Q:** What is a dependency in Terraform?  
**A:** Resources that rely on others (implicit or explicit).  

**Q:** How do you lock state?  
**A:** Use a remote backend with locking (e.g., DynamoDB).  

### Destruction
**Q:** How do you destroy infrastructure?  
**A:** Use `terraform destroy`.  

---

## Ansible (30 Questions)

### Basics
**Q:** What is Ansible?  
**A:** An open-source tool for configuration management and automation.  

**Q:** How do you install Ansible?  
**A:** Use `pip install ansible` or package managers (e.g., `apt`).  

### Playbooks & Tasks
**Q:** What is a playbook?  
**A:** A YAML file defining automation tasks.  

**Q:** What is a task?  
**A:** A single action in a playbook (e.g., install package).  

**Q:** How do you run a playbook?  
**A:** Use `ansible-playbook <playbook.yml>`.  

### Inventory & Hosts
**Q:** What is an inventory file?  
**A:** Lists hosts Ansible manages.  

**Q:** How do you ping hosts?  
**A:** Use `ansible all -m ping`.  

**Q:** How do you limit hosts?  
**A:** Use `-l <host-pattern>` with `ansible-playbook`.  

### Modules & Idempotency
**Q:** What is a module in Ansible?  
**A:** A predefined task (e.g., `file`, `yum`).  

**Q:** What is idempotency in Ansible?  
**A:** Tasks only apply changes if needed.  

### Variables & Templates
**Q:** What is a variable in Ansible?  
**A:** A value used in playbooks (e.g., `{{ var_name }}`).  

**Q:** What is a template?  
**A:** A file with Jinja2 syntax for dynamic content.  

**Q:** How do you copy files?  
**A:** Use the `copy` module (e.g., `copy: src= dest=`).  

### Roles & Galaxy
**Q:** What is a role?  
**A:** A reusable set of tasks, variables, and files.  

**Q:** What is Ansible Galaxy?  
**A:** A repository for sharing roles.  

**Q:** How do you install a role?  
**A:** Use `ansible-galaxy install <role-name>`.  

### Handlers & Conditionals
**Q:** What is a handler?  
**A:** A task triggered by a change (e.g., restart service).  

**Q:** What is a condition in Ansible?  
**A:** Uses `when` to run tasks conditionally.  

### Privileges & Debugging
**Q:** What is `become` in Ansible?  
**A:** Escalates privileges (e.g., `sudo`).  

**Q:** How do you debug in Ansible?  
**A:** Use the `debug` module (e.g., `debug: msg="{{ var }}"`).  

### Vault & Security
**Q:** What is a vault?  
**A:** Encrypts sensitive data (e.g., `ansible-vault encrypt`).  

### Testing & Dry Runs
**Q:** How do you dry-run a playbook?  
**A:** Use `--check` with `ansible-playbook`.  

**Q:** How do you test connectivity?  
**A:** Use `ansible all -m ping -u <user>`.  

### Advanced Features
**Q:** What is a fact?  
**A:** System info gathered from hosts (e.g., OS version).  

**Q:** What is a loop in Ansible?  
**A:** Repeats tasks with `loop` or `with_items`.  

**Q:** What is a playbook import?  
**A:** Includes another playbook with `import_playbook`.  

### Ansible Tower
**Q:** What is Ansible Tower?  
**A:** A web-based UI for managing Ansible (now AWX).  

---

## Prometheus & Grafana (20 Questions)

### Prometheus Basics
**Q:** What is Prometheus?  
**A:** An open-source monitoring and alerting system.  

**Q:** How does Prometheus collect metrics?  
**A:** Scrapes HTTP endpoints exposing metrics.  

**Q:** What is a Prometheus exporter?  
**A:** A tool exporting app/system metrics (e.g., Node Exporter).  

### Configuration & Querying
**Q:** How do you configure Prometheus?  
**A:** Edit `prometheus.yml` with scrape targets.  

**Q:** What is PromQL?  
**A:** Prometheus Query Language for querying metrics.  

**Q:** What is a scrape interval?  
**A:** How often Prometheus collects metrics (e.g., `15s`).  

### Alerting
**Q:** What is an alert rule?  
**A:** A condition triggering notifications (e.g., high CPU).  

**Q:** What is Alertmanager?  
**A:** Handles Prometheus alerts (e.g., sends to Slack).  

### Grafana Basics
**Q:** What is Grafana?  
**A:** A visualization tool for metrics from Prometheus and other sources.  

**Q:** How do you add a data source in Grafana?  
**A:** Configure it in Grafana UI under "Data Sources."  

**Q:** What is a dashboard in Grafana?  
**A:** A visual representation of metrics.  

### Metrics & Data
**Q:** What is a time series?  
**A:** Data points collected over time, stored in Prometheus.  

**Q:** What is a label in Prometheus?  
**A:** A key-value pair for filtering metrics.  

**Q:** What is a counter metric?  
**A:** A cumulative value that only increases (e.g., requests).  

**Q:** What is a gauge metric?  
**A:** A value that can go up or down (e.g., CPU usage).  

### Installation & Security
**Q:** How do you install Prometheus?  
**A:** Download and run the binary or use Docker.  

**Q:** How do you secure Prometheus?  
**A:** Use reverse proxies or basic auth.  

### Visualization
**Q:** How do you visualize Prometheus data?  
**A:** Connect it to Grafana and create dashboards.  

**Q:** How do you import a dashboard?  
**A:** Use Grafana's JSON import feature.  

### Status Checks
**Q:** How do you check Prometheus status?  
**A:** Access `/metrics` or `/status` on its port (default `9090`).  

# Part 4: ELK Stack, Bash Scripting, Python Scripting, Rancher, Helm, Operators

## ELK Stack (20 Questions)

### Core Components
**Q:** What is the ELK Stack?  
**A:** Elasticsearch, Logstash, and Kibana for logging and observability.  

**Q:** What is Elasticsearch?  
**A:** A distributed search and analytics engine for storing logs.  

**Q:** What is Logstash?  
**A:** A tool for collecting, processing, and forwarding logs.  

### Installation & Setup
**Q:** How do you install ELK?  
**A:** Download and configure each component or use Docker.  

**Q:** How do you secure ELK?  
**A:** Enable X-Pack security with authentication and SSL.  

### Elasticsearch
**Q:** What is an index in Elasticsearch?  
**A:** A collection of documents with similar characteristics.  

**Q:** What is a document in Elasticsearch?  
**A:** A JSON object stored in an index.  

**Q:** What is a shard in Elasticsearch?  
**A:** A subset of an index for scalability.  

### Logstash
**Q:** How does Logstash process logs?  
**A:** Uses pipelines with input, filter, and output stages.  

**Q:** What is a pipeline in Logstash?  
**A:** A configuration defining log processing flow.  

**Q:** What is a filter in Logstash?  
**A:** Transforms log data (e.g., grok for parsing).  

### Kibana
**Q:** What is Kibana?  
**A:** A visualization tool for Elasticsearch data.  

**Q:** What is a Kibana dashboard?  
**A:** A visual representation of log data.  

**Q:** How do you create a visualization in Kibana?  
**A:** Use the Visualize tab with an index pattern.  

### Beats & Integration
**Q:** What is Filebeat?  
**A:** A lightweight shipper for sending logs to Logstash or Elasticsearch.  

**Q:** How do you send logs to Logstash?  
**A:** Use agents like Filebeat or direct inputs (e.g., TCP).  

### Querying & Monitoring
**Q:** How do you query Elasticsearch?  
**A:** Use REST API or Kibana's query language (e.g., Lucene).  

**Q:** How do you monitor ELK performance?  
**A:** Use Kibana's Monitoring UI or API endpoints.  

### Scaling & Patterns
**Q:** How do you scale Elasticsearch?  
**A:** Add nodes to the cluster and configure replicas.  

**Q:** What is an index pattern in Kibana?  
**A:** A way to map Elasticsearch indices for visualization.  

---

## Bash Scripting (30 Questions)

### Basics
**Q:** What is a Bash script?  
**A:** A file with shell commands, starting with `#!/bin/bash`.  

**Q:** How do you make a script executable?  
**A:** Use `chmod +x <script.sh>`.  

### Variables & Output
**Q:** What is a variable in Bash?  
**A:** A named value (e.g., `name="John"`).  

**Q:** How do you print a variable?  
**A:** Use `echo $name` or `echo ${name}`.  

### Control Flow
**Q:** What is a conditional statement?  
**A:** Uses `if [ condition ]; then ... fi` for logic.  

**Q:** What is a case statement?  
**A:** A switch-like construct (e.g., `case $var in ... esac`).  

### Loops
**Q:** How do you loop over a list?  
**A:** Use `for item in list; do echo $item; done`.  

**Q:** What is a while loop?  
**A:** Repeats while a condition is true (e.g., `while [ $i -lt 5 ]; do ... done`).  

### Arguments & Input
**Q:** What is `$1` in a script?  
**A:** The first command-line argument.  

**Q:** How do you read user input?  
**A:** Use `read -p "Prompt: " var`.  

### File Operations
**Q:** How do you check if a file exists?  
**A:** Use `[ -f file ] && echo "exists"`.  

**Q:** How do you append to a file?  
**A:** Use `echo "text" >> file`.  

### Text Processing
**Q:** What is `grep` in a script?  
**A:** Searches for patterns (e.g., `grep "error" log.txt`).  

**Q:** What is `awk` in Bash?  
**A:** Processes text (e.g., `awk '{print $1}' file`).  

### Functions & Debugging
**Q:** What is a function in Bash?  
**A:** A reusable block of code (e.g., `func() { echo hi; }`).  

**Q:** How do you debug a script?  
**A:** Use `bash -x script.sh` for step-by-step output.  

### Advanced Features
**Q:** What is a trap?  
**A:** Catches signals (e.g., `trap 'echo exit' EXIT`).  

**Q:** What is `xargs`?  
**A:** Builds commands from input (e.g., `echo "file" | xargs ls`).  

---

## Python Scripting (30 Questions)

### Basics
**Q:** What is Python?  
**A:** A high-level, interpreted programming language.  

**Q:** How do you run a Python script?  
**A:** Use `python script.py` or `python3 script.py`.  

### Data Structures
**Q:** What is a list?  
**A:** An ordered, mutable collection (e.g., `lst = [1, 2, 3]`).  

**Q:** What is a dictionary?  
**A:** A key-value collection (e.g., `d = {"key": "value"}`).  

### Control Flow
**Q:** What is an `if` statement?  
**A:** Uses `if condition: ... elif: ... else: ...`.  

**Q:** What is a `while` loop?  
**A:** Repeats while true (e.g., `while x < 5: x += 1`).  

### Functions & Modules
**Q:** How do you define a function?  
**A:** Use `def func(): print("hi")`.  

**Q:** What is a module?  
**A:** A file with Python code (e.g., `import os`).  

### File Handling
**Q:** How do you read a file?  
**A:** Use `with open("file.txt", "r") as f: content = f.read()`.  

**Q:** How do you write to a file?  
**A:** Use `with open("file.txt", "w") as f: f.write("text")`.  

### Error Handling
**Q:** How do you handle exceptions?  
**A:** Use `try: ... except Exception as e: print(e)`.  

### Advanced Features
**Q:** What is a lambda function?  
**A:** An anonymous function (e.g., `lambda x: x + 1`).  

**Q:** What is `__main__`?  
**A:** The entry point of a script (e.g., `if __name__ == "__main__":`).  

---

## Rancher (20 Questions)

### Basics
**Q:** What is Rancher?  
**A:** An open-source platform for managing Kubernetes clusters.  

**Q:** How do you install Rancher?  
**A:** Use Docker: `docker run -d --restart=unless-stopped -p 80:80 -p 443:443 rancher/rancher`.  

### Cluster Management
**Q:** What is a Rancher cluster?  
**A:** A Kubernetes cluster managed by Rancher.  

**Q:** How do you add a cluster in Rancher?  
**A:** Use the UI to import or create a cluster with RKE.  

### Projects & Apps
**Q:** What is a project in Rancher?  
**A:** A logical grouping of namespaces.  

**Q:** How do you deploy an app in Rancher?  
**A:** Use the UI's "Deploy" or Helm charts.  

---

## Helm (20 Questions)

### Basics
**Q:** What is Helm?  
**A:** A package manager for Kubernetes.  

**Q:** What is a Helm chart?  
**A:** A collection of files defining a Kubernetes app.  

### Operations
**Q:** How do you install a chart?  
**A:** Use `helm install <release-name> <chart>`.  

**Q:** How do you upgrade a release?  
**A:** Use `helm upgrade <release-name> <chart>`.  

---

## Operators (20 Questions)

### Basics
**Q:** What is a Kubernetes Operator?  
**A:** A custom controller managing app lifecycle.  

**Q:** What is a Custom Resource (CR)?  
**A:** An extension of Kubernetes API managed by an Operator.  

### Development
**Q:** How do you create an Operator?  
**A:** Use `operator-sdk init` and define CRDs.  

**Q:** What is reconciliation in Operators?  
**A:** Aligning current state with desired state.  

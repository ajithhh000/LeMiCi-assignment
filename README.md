
---

# LeMiCi Assignment

## Part 1

1. **Done**

2. **Explain `git fetch` vs `git pull` and how to resolve merge conflicts**  
   - `git fetch` downloads the latest changes from the remote repository into your local remote-tracking branches but **does not modify** your working directory or current branch. It lets you inspect incoming changes before integrating them.  
   - `git pull` is a combination of `git fetch` followed immediately by `git merge`. It fetches changes and **automatically merges** them into your current branch, which can sometimes result in merge conflicts.

   **Steps to resolve merge conflicts**:  
   - Merge conflicts occur when two branches modify the same lines of code differently.  
   - Identify conflict markers in the file: `<<<<<<<`, `=======`, `>>>>>>>`.  
   - Manually edit the file to keep the desired changes and remove the markers.  
   - Stage the resolved file:  
     ```bash
     git add <filename>
     ```  
   - Complete the merge with a commit:  
     ```bash
     git commit
     ```

3. **Performed and resolved a merge conflict**  
   Used two branches: `branchA` and `branchB`.

---

## Part 2

1. **Done**

2. **Docker Concepts & Best Practices**  
   - **Dockerfile**: A text file containing step-by-step instructions to build a Docker image.  
   - **Docker Image**: A lightweight, standalone, executable package (template/blueprint) built from a Dockerfile.  
   - **Docker Container**: A running instance of a Docker image. Containers are isolated and use system resources directly.

   **Optimization Best Practices**:  
   - ✅ **Use minimal base images**: Replace `python:3.10` with `python:3.10-alpine` for smaller size.  
   - ✅ **Combine `RUN` commands**:  
     ```dockerfile
     # Instead of:
     RUN apt update
     RUN apt install -y package

     # Use:
     RUN apt update && apt install -y package && rm -rf /var/lib/apt/lists/*
     ```  
   - ✅ **Use `.dockerignore`**: Exclude unnecessary files (e.g., logs, docs, `node_modules`).  
   - ✅ **Remove pip cache**: Use `--no-cache-dir` in pip installs to avoid storing temporary files.

3. **Done**

---

## Part 3

1. **Difference Between Pod, Deployment, and Service**  
   - **Pod**: The smallest deployable unit in Kubernetes. It runs one or more tightly coupled containers, shares network/storage, and has a unique IP. Pods are ephemeral—Kubernetes replaces them if they fail.  
   - **Deployment**: Manages a set of identical Pods. Ensures the desired number of replicas are running, supports rolling updates, scaling, and self-healing. Maintains the application’s desired state.  
   - **Service**: Provides a stable network endpoint (IP/DNS) to access a group of Pods. Since Pod IPs change dynamically, Services enable reliable load balancing and discovery.

   > **In short**:  
   > - **Pod** → runs your app containers  
   > - **Deployment** → manages Pods  
   > - **Service** → exposes Pods to the network

2. **Why use Amazon EKS over self-managed Kubernetes?**  
   Amazon Elastic Kubernetes Service (EKS) is a fully managed Kubernetes service by AWS that offers:  
   - ✅ Automated control plane management  
   - ✅ Built-in high availability  
   - ✅ Seamless integration with AWS services (IAM, VPC, CloudWatch, etc.)  
   - ✅ Simplified version upgrades and patching  
   - ✅ Enhanced security and compliance support  

   This allows teams to focus on **application development** instead of cluster operations.

3. **Done**

---

## Part 4

1. **Done**

2. **GitHub Actions Workflow Explanation**  
   The workflow:  
   - Triggers on every `push` to the `main` branch.  
   - Builds the Docker image using the provided `Dockerfile`.  
   - Runs a placeholder test (`echo "Tests passed"`).  
   - Simulates pushing the image to DockerHub (no real credentials or push commands included).  

   This satisfies the assignment requirements.  
   > 💡 *To extend for Kubernetes deployment, add `kubectl apply` or Helm steps after testing.*

---

## Part 5

1. **Difference between metrics, logs, and traces**  
   - **Metrics**: Numerical measurements of system performance (e.g., CPU usage, request rate).  
   - **Logs**: Timestamped records of events, errors, or debug info from applications.  
   - **Traces**: End-to-end tracking of a request as it flows through multiple services (used in distributed systems).

2. **How to debug a crashed Kubernetes Pod**  
   - Check pod description:  
     ```bash
     kubectl describe pod <pod-name>
     ```  
   - View current and previous logs:  
     ```bash
     kubectl logs <pod-name> --previous
     ```  
   - Inspect cluster events:  
     ```bash
     kubectl get events --sort-by=.metadata.creationTimestamp
     ```

3. **Monitoring tools for AWS EKS**  
   - **Prometheus + Grafana**: For custom metrics and dashboards.  
   - **Amazon CloudWatch**: Native AWS monitoring, logs, and alarms.  
   - **ELK Stack (Elasticsearch, Logstash, Kibana)**: For centralized log aggregation and analysis.

---

## Part 6

**End-to-End Deployment Plan for EKS**

1. Clone the application source code from the GitHub repository.  
2. Containerize the app by creating a `Dockerfile` and building a Docker image.  
3. Push the image to a container registry (e.g., DockerHub or AWS ECR).  
4. Create a Kubernetes **Deployment** YAML to define:  
   - Number of replicas  
   - Container image  
   - Resource limits  
5. Set up a **GitHub Actions CI/CD pipeline** that:  
   - Builds and tests the app on `main` branch pushes  
   - Pushes the Docker image to the registry  
   - Deploys the updated app to EKS using `kubectl` or Helm  
6. Configure **centralized logging** (e.g., Fluentd + CloudWatch or ELK) so logs are visible to the dev team.  
7. Implement **monitoring** using CloudWatch, Prometheus, or Grafana to track app health and performance.

--- 

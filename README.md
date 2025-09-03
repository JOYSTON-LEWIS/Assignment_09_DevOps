# Assignment 09 - DevOps: JENKINS CI / CD for Microservice Application

This project demonstrates a complete **DevOps pipeline and infrastructure automation** for a **MERN microservices application**, deployed on AWS using **Docker, ECR, EC2, Auto Scaling Groups, Load Balancers, Lambda, EKS (Kubernetes), Helm, and CloudWatch**.

---

## 📌 Project Repository
- Forked Project Repository: [SampleMERNwithMicroservices](https://github.com/UnpredictablePrashant/SampleMERNwithMicroservices)

---

## 🚀 Steps Implemented

### **Step 1: AWS Environment Setup**
- Installed and configured **AWS CLI** with IAM credentials.
- Installed and configured **Boto3** for Python-based AWS automation.

---

### **Step 2: Prepare the MERN Application**
1. **Containerization**
   - Created `Dockerfile` for both **frontend** and **backend**.
   - Verified local builds with `docker build` and `docker run`.

2. **Push Images to Amazon ECR**
   - Created ECR repositories for:
     - `mern-frontend`
     - `mern-backend`
   - Built and pushed Docker images to ECR:
     ```bash
     docker build -t <account_id>.dkr.ecr.ap-south-1.amazonaws.com/mern-frontend:latest ./frontend
     docker build -t <account_id>.dkr.ecr.ap-south-1.amazonaws.com/mern-backend:latest ./backend
     docker push <account_id>.dkr.ecr.ap-south-1.amazonaws.com/mern-frontend:latest
     docker push <account_id>.dkr.ecr.ap-south-1.amazonaws.com/mern-backend:latest
     ```

---

### **Step 3: Version Control**
- Used **GitHub** (instead of AWS CodeCommit).
- Set up repository triggers for CI/CD pipelines.

---

### **Step 4: Continuous Integration**
- Jenkins server was already provided.
- Configured pipelines for:
  - Building and pushing Docker images to ECR.
  - Automated deployment triggers on new commits to GitHub.

---

### **Step 5: Infrastructure as Code (IaC) with Boto3**
- Defined AWS infrastructure using Python + Boto3 scripts:
  - **VPC, Subnets, Security Groups**
  - **Auto Scaling Group (ASG)** for backend EC2 instances
  - **IAM Roles and Policies**
  - **S3 Buckets** for backups and storage

---

### **Step 6: Backend Deployment**
- Provisioned **EC2 instances** via ASG.
- Pulled **backend Docker image** from ECR.
- Deployed containerized backend application across instances.

---

### **Step 7: Networking Setup**
- Configured **Elastic Load Balancer (ELB)** for backend ASG.
- Integrated with **Route 53 DNS** for domain-based access.

---

### **Step 8: Frontend Deployment**
- Provisioned dedicated **EC2 instances**.
- Pulled **frontend Docker image** from ECR.
- Served frontend application and connected it to backend API through Load Balancer.

---

### **Step 9: AWS Lambda Deployment**
- Created Lambda functions for:
  - **Automated Database Backups** (MongoDB Atlas / RDS snapshots).
  - Stored backups in **S3 bucket** with timestamped filenames.
- Lambda written in **Python (Boto3 + pymongo)**.

---

### **Step 10: Kubernetes (EKS) Deployment**
1. **Cluster Setup**
   - Created EKS cluster using `eksctl`.
   - Configured `kubectl` and `aws-auth` mappings.

2. **Helm Deployment**
   - Packaged **frontend** and **backend** services into Helm charts.
   - Installed via:
     ```bash
     helm install backend ./helm/backend
     helm install frontend ./helm/frontend
     ```
   - Configured Ingress Controller for unified access.

---

### **Step 11: Monitoring & Logging**
- **CloudWatch Monitoring**
  - Configured metrics for EC2, EKS nodes, and ASG scaling policies.
  - Alarms for CPU, Memory, and Health Checks.

- **CloudWatch Logs**
  - Aggregated logs from EC2, Lambda, and Kubernetes Pods.
  - Enabled centralized log retention.

---

### **Step 12: Documentation**
- This **README.md** serves as the primary documentation.
- Architecture and deployment process are fully documented in repository.

---

### **Step 13: Final Validation**
- Verified:
  - Frontend accessible via DNS.
  - Backend APIs functional.
  - Auto Scaling triggered on load.
  - Database backups stored in S3.

---

## 🏗️ High-Level Architecture

```text
      +----------------+
      |   GitHub Repo  |
      +-------+--------+
              |
              v
        +-------------+
        |   Jenkins   |
        +------+------+     
               |
    ---------------------------
    |                         |
    v                         v
+------------------+     +------------------+
| Build Docker Img |     | Boto3 Infra IaC  |
+------------------+     +------------------+
        |                         |
        v                         v
+------------------+     +------------------+
|    Push to ECR   |     |  Deploy EC2/ASG  |
+------------------+     +------------------+
        |                         |
        +-----------+-------------+
                    |
                    v
            +---------------+
            | Load Balancer |
            +-------+-------+
                    |
        ----------------------------
        |                          |
        v                          v
+-----------------+        +-----------------+
|  Frontend EC2   |        | Backend ASG EC2 |
+-----------------+        +-----------------+

   +-----------------------------------------+
   |   EKS Cluster + Helm (Frontend/Backend) |
   +-----------------------------------------+

   +-----------------------------------------+
   |  Lambda (DB Backups) → S3 (timestamped) |
   +-----------------------------------------+

   +-----------------------------------------+
   |     CloudWatch Monitoring & Logging     |
   +-----------------------------------------+

```


---

## ✅ Achievements
- MERN Application successfully containerized and deployed.
- Automated CI/CD with Jenkins and GitHub.
- Infrastructure as Code with **Boto3**.
- Backend scaling with **ASG + ELB**.
- Frontend and Backend deployed on **EKS** with **Helm**.
- Automated **DB backups via Lambda → S3**.
- Centralized **Monitoring & Logging with CloudWatch**.

---

### 📸 Screenshots:

<img width="1918" height="961" alt="image" src="https://github.com/user-attachments/assets/ac850857-0252-4093-b823-5b6d5b9e5ca6" />
<img width="1918" height="292" alt="image" src="https://github.com/user-attachments/assets/e2f635e8-65bf-4af2-8e3b-7e7562a3a4b1" />
<img width="1917" height="235" alt="image" src="https://github.com/user-attachments/assets/555e9628-abc3-4ee7-811a-444ed7ba61ea" />

## 📜 License
This project is licensed under the MIT License.

## 🤝 Contributing
Feel free to fork and improve the scripts! ⭐ If you find this project useful, please consider starring the repo—it really helps and supports my work! 😊

## 📧 Contact
For any queries, reach out via GitHub Issues.

---

🎯 **Thank you for reviewing this project! 🚀**


# Deploying 2048 Game on Amazon EKS

This project demonstrates how to deploy a containerized application on **Amazon Elastic Kubernetes Service (EKS)** and expose it to the internet using the **AWS Load Balancer Controller**.

The application used in this project is the classic **2048 game**, deployed using Kubernetes resources.

---

## 📌 Project Overview

The goal of this project is to understand how Kubernetes works with AWS to deploy scalable applications. The application is deployed inside a Kubernetes cluster running on Amazon EKS and accessed externally through an **Application Load Balancer (ALB)**.

---

## 🏗 Architecture

User → AWS Application Load Balancer → Kubernetes Ingress → Kubernetes Service → Pods (2048 Game)

---

## ⚙️ Tech Stack

- **AWS EKS** – Managed Kubernetes cluster
- **Docker** – Containerized application
- **Kubernetes** – Deployment, Service, Ingress
- **AWS Load Balancer Controller** – To create and manage ALB
- **kubectl** – Kubernetes CLI tool
- **IAM** – Role and permissions management

---

## 🚀 Deployment Steps

### 1. Create EKS Cluster
Create the Kubernetes cluster on AWS.

```bash
eksctl create cluster --name 2048-cluster --region us-east-1
```

---

### 2. Configure kubectl

```bash
aws eks update-kubeconfig --name 2048-cluster --region us-east-1
```

Verify cluster connection:

```bash
kubectl get nodes
```

---

### 3. Install AWS Load Balancer Controller

Create IAM policy for the controller and attach it to the service account.

```bash
curl -o iam_policy.json https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/main/docs/install/iam_policy.json
```

Create policy:

```bash
aws iam create-policy \
--policy-name AWSLoadBalancerControllerIAMPolicy \
--policy-document file://iam_policy.json
```

---

### 4. Deploy the 2048 Application

Apply the Kubernetes manifests.

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/main/docs/examples/2048/2048_full.yaml
```

---

### 5. Verify Deployment

Check pods:

```bash
kubectl get pods -n game-2048
```

Check services:

```bash
kubectl get svc -n game-2048
```

Check ingress:

```bash
kubectl get ingress -n game-2048
```

---

## 🌐 Access the Application

After deployment, the AWS Load Balancer Controller will automatically create an **Application Load Balancer**.

Retrieve the ALB DNS name:

```bash
kubectl get ingress -n game-2048
```

Open the DNS URL in the browser to play the **2048 game**.

---

## 📸 Screenshots

Add screenshots here:

- Running 2048 game in browser
- Kubernetes pods
- ALB created in AWS console

---

## 🎯 Key Learnings

- Deploying applications on **Amazon EKS**
- Managing Kubernetes resources with **kubectl**
- Integrating **AWS Load Balancer Controller**
- Understanding Kubernetes **Ingress and Services**
- Exposing applications using **Application Load Balancer**

---

## 📌 Future Improvements

- Automate infrastructure using **Terraform**
- Add **CI/CD pipeline (GitHub Actions / Jenkins)**
- Enable **monitoring with Prometheus & Grafana**
- Implement **auto-scaling**

---

## 👨‍💻 Author

**Thanushkumar**

DevOps Enthusiast | AWS | Kubernetes | Terraform | Docker

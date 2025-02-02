# Kubernetes Deployment with Ansible Automation

This repository contains all the necessary files and instructions to set up a Kubernetes cluster using Minikube, deploy an Nginx ingress controller, and deploy a "Hello World" application. The entire setup is automated using Ansible playbooks.

## Table of Contents

1. [Pre-requisite](#Pre-requisite)
2. [Kubernetes Cluster Setup](#kubernetes-cluster-setup)
3. [Nginx Ingress Setup](#nginx-ingress-setup)
4. [Sample Application Deployment](#sample-application-deployment)
5. [Security with TLS/SSL](#security-with-tlsssl)
6. [Ansible Automation](#ansible-automation)
7. [Repository Structure](#repository-structure)

## Pre-requisite

1. **Ansible**
2. **Docker**
3. **Kubectl**
4. **Helm**
5. **Minikube**

**To install above run script-to-install-ansible.sh & setup-tools.yaml scripts**

**Setup required tools:**

```bash
bash script-to-install-ansible.sh
ansible-playbook setup-tools.yaml
```

## Kubernetes Cluster Setup

To create a local Kubernetes cluster using Minikube:

1. **Install Minikube:**

   ```bash
   curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube_latest_amd64.deb
   sudo dpkg -i minikube_latest_amd64.deb
   ```
2. **Start Minikube:**

   ```bash
   minikube start --force
   ```

## Nginx Ingress Setup

To install the Nginx ingress controller using Helm:

1. **Add Helm repository:**

   ```bash
   helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
   helm repo update
   ```
2. **Install the Nginx ingress controller:**

   ```bash
   helm install my-nginx-ingress ingress-nginx/ingress-nginx
   ```

## Sample Application Deployment

Deploy the "Hello World" application:

1. **Create Kubernetes manifests:**

   - `deployment.yaml`
   - `service.yaml`
   - `ingress.yaml`
2. **Apply the manifests:**

   ```bash
   kubectl apply -f deployment.yaml
   kubectl apply -f service.yaml
   kubectl apply -f ingress.yaml
   ```
3. 

## Security with TLS/SSL

The playbook also handles TLS termination using a self-signed certificate.

1. **Generate self-signed certificate:**

   ```bash
   openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout tls.key -out tls.crt -subj "/CN=example.com/O=example.com"
   ```
2. **Create Kubernetes secret:**

   ```bash
   kubectl create secret tls tls-secret --key tls.key --cert tls.crt
   ```

## Ansible Automation

### How to Run the Ansible Playbook

1. **Run the main playbook:**

   ```bash
   ansible-playbook playbook.yaml
   ```
2. **Access the application:**

   - Visit `https://example.com` in your web browser.

### Troubleshooting

- **Issue:** Minikube fails to start.
  - **Solution:** Ensure virtualization is enabled on your machine.
- **Issue:** Nginx ingress controller fails to deploy.
  - **Solution:** Check Helm logs for detailed error messages.
- **Issue:** Application not accessible via ingress.
  - **Solution:** Verify the ingress and service configurations.

## Repository Structure

* `deployment.yaml`: Kubernetes deployment manifest for the "Hello World" application.
* `service.yaml`: Kubernetes service manifest for the "Hello World" application.
* `ingress.yaml`: Kubernetes ingress manifest to expose the "Hello World" application.
* `playbook.yaml`: Ansible playbook to automate the deployment process.
* `rollback-playbook.yaml`: Ansible playbook to rollback the deployment.
* `script-to-install-ansible.sh`: Script to install Ansible.
* `setup-tools.yaml`: Ansible playbook to install necessary tools (Docker, kubectl, Helm, Minikube).

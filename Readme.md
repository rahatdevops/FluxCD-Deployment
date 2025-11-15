✅ Overview

This setup deploys WordPress + MySQL into Kubernetes using FluxCD GitOps, SOPS encryption, and Kustomize. All manifests are stored in a Git repository, and Flux automatically applies updates.

🚀 Deployment Flow (Short Summary)

FluxCD installed in the cluster – handles Git sync + reconciliation.

Git repository created – contains WordPress, MySQL manifests, Secrets, and Kustomization files.

SOPS + Age used to encrypt secrets – secure passwords in Git.

Flux Git source created – points cluster to your Git repo.

Flux Kustomization created – applies all YAML files inside the repo.

Flux automatically deploys:

MySQL Deployment + Service

WordPress Deployment + Service

Optional Ingress

Encrypted Kubernetes Secrets

🔍 Key Components
📌 1. MySQL

Runs as a Deployment

Uses Kubernetes Secret for credentials

Exposed via ClusterIP service

📌 2. WordPress

Connects to MySQL via environment variables from Secret

Exposed via Service (ClusterIP or LoadBalancer)

📌 3. FluxCD

Watches your Git repo

Applies any changes automatically

Ensures cluster state matches Git state

🔐 Secret Handling (Short)

Secrets stored as YAML

Encrypted using SOPS (Age key)

Flux decrypts them during reconciliation

🛠 Verification Commands

Check all pods:

kubectl get pods -A

Check services:

kubectl get svc -A

Trigger immediate sync:

flux reconcile kustomization flux-system

Check Flux sync status:

flux get kustomizations
🎯 Deployment Result

After the reconciliation:

WordPress is deployed and running

MySQL is deployed and reachable inside the cluster

Secrets are securely decrypted

Ingress (optional) exposes WordPress via domain

All updates are automated via GitOps

📌 Summary in One Line

"Push to Git → Flux auto-syncs → Cluster updates automatically."

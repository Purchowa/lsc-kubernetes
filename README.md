# EKS Setup and NFS Provisioner Deployment Guide

## 0. Create a Node Group in EKS

After creating the EKS cluster, make sure to create a **Node Group** inside EKS cluster. Without it, the cluster will not be able to run any workloads.

## 1. Configure Connection to EKS

```bash
aws eks describe-cluster --region us-east-1 --name lsc-lab6 --query cluster.status
aws eks --region us-east-1 update-kubeconfig --name lsc-lab6
```

## 2. Add Helm Repository

```bash
helm repo add nfs-ganesha-server-and-external-provisioner https://kubernetes-sigs.github.io/nfs-ganesha-server-and-external-provisioner
helm repo update
```

## 3. Install the NFS Provisioner Chart and verify it

```bash
helm install lsc-nfs nfs-ganesha-server-and-external-provisioner/nfs-server-provisioner --set storageClass.name=nfs --set storageClass.defaultClass=true
kubectl get storageclass # verification
```

## 5. Apply Kubernetes Configuration located in `configuration` directory

```bash
kubectl apply -f ./configuration
```

## 6. Verify Everything Is Running

```bash
kubectl get all
```

Everything should have a running state.
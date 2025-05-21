# Azure-Kubernetes-Service
Deploy an E-Commerce Project on Azure Kubernetes Service | Step By Step Guide Project AKS


Deploy an E-Commerce Project on Azure Kubernetes Service | Step By Step Guide Project AKS

This is MicroService Application that need deployment which will need to
1. Dockerized each of the containers with the Dockerfiles
2. Use the k8s manifest
3. Helm
4. Akp

Helm 3 important
1. Chat.yml
2. Template folder
3. Values.yml

Azure Cloud
Create Kubernetes Cluster
Steps

Kubernetes service
Click on create kubernetes cluster
Create resource group
Select location Germany 
Kubernetes cluster name “three-tire”
AKS pricing tier “free”
Kubernetes version default
Automatic upgrade default
Automatic upgrade scheduler default
Node security channel type default
Security channel scheduler default
Authentication and Authorization default

Steps 2 
Next
Click on nodeAgent

Steps
Go to Terminal
Git clone https://github.com/iam-veeramalla/three-tier-architecture-demo
Cd three-tier-architecture-demo
az login
Enter 1 and press enter
az aks get-credentials --resource-group ecommerce-demo --name three-tier  
kubectl get nodes
kubectl get pods
kubectl config current-context
cd AKS
ls
cd helm
ls

https://github.com/iam-veeramalla/three-tier-architecture-demo/tree/master/AKS/helm
Copy this code below there

kubectl create ns robot-shop

helm install robot-shop --namespace robot-shop .

kubectl get storageclass

NOTE THIS AZURE HAS 2 STORAGE
1. Azure file {EFS ON AWS}
2. Azure Disk{EBS ON WAS} When to used this is when it a single pods

kubectl describe pod redis-0 -n robot-shop


 kubectl get pvc -n robot-shop

kubectl get pods -n robot-shop

kubectl get svc -n robot-shop


Step for ingress
Go to azure portal under the three-trie
Go to networking
Enable ingress controller > apply                  ingress was not able to enable 
Run this below

✅ Step 1: Add the Ingress NGINX Helm repo
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx

Then update your local Helm repo list
helm repo update


✅ Step 2: Re-run the installation command
helm install nginx-ingress ingress-nginx/ingress-nginx \
  --create-namespace \
  --namespace ingress-nginx \
  --set controller.publishService.enabled=true

✅ Step 3: Check if it deployed correctly
After the install, verify the resources:
kubectl get all -n ingress-nginx


You should see pods like:
* nginx-ingress-controller-...
* A LoadBalancer type service with an external IP


Steps
kubectl apply -f ingress.yaml -n robot-shop
kubectl get pods -n kube-system              I was not able to find ingress 
kubectl get ingress -n robot-shop



A demonstration of deploying to the Azure Kubernetes Service (AKS). The target app is a simple microservice app in ASP.NET Core.

## Deploy ASP.NET Core microservices app to Azure Kuberentes Service

#### Push your image to the docker registry
```
docker login

docker tag firstmicroservice viktorija11/firstmicroservice

docker push viktorija11/firstmicroservice 
```
#### Create Azure Resource Group with an Azure Kuberenetes Cluster as a resource
```
az group create --name FirstMicroserviceResources --location westus

az account set -s 5e73ce8c-9153-4b71-baa6-c56715fc0451

az aks create --resource-group FirstMicroserviceResources --name  FirstMicroserviceCluster --node-count 1 --enable-addons http_application_routing --generate-ssh-keys
```
#### Download AKS credentials file so that we can deplot in the cloud
```
az aks get-credentials --resource-group FirstMicroserviceResources --name FirstMicroserviceCluster
```
#### Ddeploy and run Kuberenetes Cluster
```
kubectl apply -f deploy.yaml
kubectl get service firstmicroservice --watch
kubectl scale --replicas=2 deployment/firstmicroservice
```
#### Delete previosly created resource group
```
az group delete -n FirstMicroserviceResources
```

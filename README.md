# HolamiBanco

# Esta es una prueba técnica para la posición de ingeniero DevOps.

# Para el despliegue de la infraestructura en Azure se realizaron los siguientes comandos:

# 1) Variables 
LOCATION="eastus"
RG="rg-holaMiBanco"
ACR_NAME="holamibancoacr"  
AKS_NAME="holaMiBanco-aks"
NODE_SIZE="Standard_B2s"    
NODE_COUNT=1

# 2) Crear Resource Group
az group create \
  --name $RG \
  --location $LOCATION

# 3) Crear ACR 
az acr create \
  --resource-group $RG \
  --name $ACR_NAME \
  --sku Basic \
  --location $LOCATION


# 4) Crear AKS 
az aks create \
  --resource-group $RG \
  --name $AKS_NAME \
  --location $LOCATION \
  --node-count $NODE_COUNT \
  --node-vm-size $NODE_SIZE \
  --enable-managed-identity \
  --generate-ssh-keys \
  --attach-acr $ACR_NAME 

# Para la preparación del AKS se realizaron los siguientes comandos


# 1)  Instalar controlador ingress nginx para controlar el tráfico externo

kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.11.1/deploy/static/provider/cloud/deploy.yaml

# 2) Verificación de ip externa del LoadBalancer para especificar en ingress.yml

kubectl get svc -n ingress-nginx

# 3) Instalar cert-manager para la generación de certificado SSL/TLS con Let's Encrypt

kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.15.3/cert-manager.yaml








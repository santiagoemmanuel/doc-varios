# Guia basica levantar en kubernetes digital Ocean 
# PHPmyadmin , mysSQL 
# app node con mongo BD
# ingress controlles 
# cert manager 
# dominio frenom.com 

## Conceptos 

##  Manager?
Cert Manager servicio que se comunica con el pod de Ingress Controller. 
Para administrar y gestionar los certificados de seguridad de los dominios definidos en Ingress Controller.

## Custom Resource Definitions 
Issuer y Cluster Issuer, que son los recursos encargados de comunicarse con el proveedor de certificados, en este caso Let's Encrypt.

# pasos1

`kubectl apply -f ./ingress/01-ns-and-sa.yaml`

## instalar ingress 
# se debe instalar helm, acualizar repos e instalar ingres 
`helm repo add nginx-stable https://helm.nginx.com/stable`
`helm repo update`
`helm install nginx-ingress nginx-stable/nginx-ingress --namespace nginx-ingress`


# crear un cluster role binding de ngnix ingress controller:
`kubectl create clusterrolebinding nginx-ingress-admin -n nginx-ingress  --clusterrole=cluster-admin  --serviceaccount=nginx-ingress:nginx-ingress`


# instalar certManager 
`kubectl create namespace cert-manager`

# cert manager
`helm repo add jetstack https://charts.jetstack.io`
`helm repo update`
`helm install cert-manager jetstack/cert-manager --namespace cert-manager --version v1.8.0 --set installCRDs=true --set webhook.securePort=10260`

`kubectl apply -f .\cert-manager\`
# chalenges 
`kubectl describe challenge`


# instalar app mongo y node
# instalar mysql  y phpmyadmin
# archivos aplicados uno por uno

# aplicar los congig maps y secrets
# aplicar los archivos en orden 
kubectl apply -f .\app1\ ...
kubectl -n app describe cert/santiage-lets-encrypt-prod-tl

# carpeta app2, contiene app mongo- node / opcional
# ingress se define en archivo   
# ingress-tls-prod.yml

# dominio
`santiage.tk`












## comandos kubernetes

# se genera token digital ocean https://kubernetes.io/docs/tasks/tools/
doctl kubernetes cluster kubeconfig save <k8s-jeso-nombre-cluster>

# conectar a diferente cluster local/remoto

- kubectl config  get-contexts 
- kubectl config  use-context docker-desktop



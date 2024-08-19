### download config file from linode and put somewhere safe

### add only owner permnission

chmod 400 ~/path/to/test-kubeconfig.yaml

### set env variable to file path

export KUBECONFIG=~/path/to/test-kubeconfig.yaml

### add bitnami charts repo to helm

helm repo add bitnami https://charts.bitnami.com/bitnami

### set config file to image

helm install mongodb --values ~/path/to/helm-demo/helm-mongodb.yaml bitnami/mongodb

### check if it's working

kubectl get all

### on linode dashboard under volumes > 3 volumes should have been created dynamicaly

### Deploy mongo express from file

kubectl apply -f ~/path/to/helm-demo/helm-mongo-express.yaml

### check if pods/service were created for mongo-express

kubectl get all

### setup ingress

### add nginex chart repo

helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx

### start ingress with external access

helm install nginx-ingress ingress-nginx/ingress-nginx --set controller.publishService.enable=true

### check if its working

kubectl get all

### a load balancer should've been dynbamically create on linode, check on dashboard

### set up ingress configuration

kubectl apply -f ./helm-ingress.yaml

### check if it was created in kubenetes

kubectl get ingress

### db data should be persistent so to check

### kill all mongodb pods

kubectl scale --replicas=0 statefulset.apps/mongodb

### wait for termination

kubectl get all

### reinstate pods

kubectl scale --replicas=3 statefulset.apps/mongodb

### wait for startup and check if data is persistent

###### Clean up

### list charts

helm ls

### unistall charts with helm

helm uninstall mongodb

### this doesnt delete the volumes in linode
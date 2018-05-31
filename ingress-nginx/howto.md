# Nginx ingree demo

## Install nginx ingress controller

```
  # see: https://kubernetes.github.io/ingress-nginx/deploy/

  # deploy nginx ingress controller. 
  kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/mandatory.yaml 

  kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/provider/baremetal/service-nodeport.yaml

```

## Install backend service 

```
# deployment
kubectl create -f tomcat-demo-deployment.yml  --namespace ingress-nginx

# clusterIP service
kubectl create -f tomcat-demo-service.yml  --namespace ingress-nginx

# make sure services work well
kubectl get services  --all-namespaces

# ssh to kubernetes node and curl (clusterIP is accessalbe only in cluster)
curl  http://<CLUSTER_IP>:<PORT>/

```


## Create ingress

```

#create ingress
kubectl create -f tomcat-demo-ingress.yaml

# make sure ingress work well.  <192.168.104.99:32409> is nginx ingress controller services node ip and node port
curl -H  "Host: tomcat.demo"   http://192.168.104.99:32409/

```
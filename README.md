# helmcharts
This repo contains helm charts for simple microservices

## Pre-requisites
- minikube running : v1.18.0
- Kubectl version : v1.17.0
- docker version : 18.06.3
- helm 3 -> https://helm.sh/docs/intro/install/

## Defaults
- k8s namespace used : default

**NOTE :** I have deployed this setup on AWS instance and running minikube with --vm-driver as None

## Steps
#### Clone this repository
```
git clone https://github.com/taherbohari/helmcharts.git
```
#### Check minikube status
```
$ minikube status
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured
timeToStop: Nonexistent
```
#### Install the helm chart. You can give any chart name of your choice
```
helm install php-app php-app/
```
eg : After installation. You will see output like this. You can get the application URL as mentioned in output.
```
$ helm install php-app php-app/
minikube : 
K8S Version : 1.20.2
Helm Version : 3.1.1
K8S Namespace : default

1. Get the application URL by running these commands:
  export NODE_PORT=$(kubectl get --namespace default -o jsonpath="{.spec.ports[0].nodePort}" services php-php-app)
  export NODE_IP=$(kubectl get nodes --namespace default -o jsonpath="{.items[0].status.addresses[0].address}")
  echo http://$NODE_IP:$NODE_PORT
```
#### Get application URL using minikube
```
minikube service list
```
eg :
```
 $ minikube service list
|-------------|------------|--------------|---------------------------|
|  NAMESPACE  |    NAME    | TARGET PORT  |            URL            |
|-------------|------------|--------------|---------------------------|
| default     | kubernetes | No node port |
| default     | php-app    | http/80      | http://192.168.49.2:30080 |
| kube-system | kube-dns   | No node port |
|-------------|------------|--------------|---------------------------|
```
#### Curl the application url
```
$ curl http://192.168.49.2:30080
<html>
 <head>
  <title>A Simple Microservice</title>
 </head>
 <body>
 <p>Hello World !!!</p>
 </body>
</html>
```
**NOTE :** You can change the contents of configmap to run php code of your choice and update the chart.

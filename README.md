# bestcloud-intro-tasks
## Installation (Assuming Minikube, Helm and Docker are installed)
### Set Local Registry within Minikube
- kubectl create -f kube-registry.yaml
- Use the most updated version from https://gist.github.com/coco98/b750b3debc6d517308596c248daf3bb1

## Deployment
### Push Flask App to Local Registry
- cd 02-dockerized-flask
- sudo docker build ./ flask-80
- sudo docker tag flask-80 localhost:5000/flask-80
- sudo docker push localhost:5000/flask-80
### Install Helm Package
- helm install flask-app-80 ./flask-app-80/ --set service.type=NodePort

## Try out the app
- export NODE_PORT=$(kubectl get --namespace default -o jsonpath="{.spec.ports[0].nodePort}" services flask-app-new)
- export NODE_IP=$(kubectl get nodes --namespace default -o jsonpath="{.items[0].status.addresses[0].address}")
- echo http://$NODE_IP:$NODE_PORT 
- echo "visit the given URL"

## Example Deployment
- ![Example Deployment.](https://raw.githubusercontent.com/ResearcherOne/bcfm-intro-tasks/master/bestcloudforme-architecture.png)

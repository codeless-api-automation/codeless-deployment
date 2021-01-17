## Kubernetes deployment files
It contains definitions for k8s deployment:
- spring dataflow server
- codeless-backend
- task monitoring

## Spring dataflow server

### dataflow server broker
#### `kubectl create -f kubernetes/kafka/` 
###### You can use `kubectl get all -l app=kafka` to verify that the deployment, pod, and service resources are running.
###### Use `kubectl delete all -l app=kafka` to clean up afterwards.

### dataflow server database
#### `kubectl create -f kubernetes/mysql/`
###### You can use `kubectl get all -l app=mysql` to verify that the deployment, pod, and service resources are running.
###### You can use `kubectl delete all,pvc,secrets -l app=mysql` to clean up afterwards.

### dataflow server
#### `kubectl create -f kubernetes/server/server-config.yaml`
#### `kubectl create -f kubernetes/server/server-svc.yaml`
#### `kubectl create -f kubernetes/server/server-deployment.yaml`
###### You can use `kubectl get all -l app=scdf-server` to verify that the deployment, pod, and service resources are running. 
###### You can use `kubectl delete all,cm -l app=scdf-server` to clean up afterwards.

### Note
###### You can use the `kubectl get svc scdf-server` command to locate the EXTERNAL_IP address assigned to scdf-server
###### If you use Minikube, you do not have an external load balancer, and the EXTERNAL_IP shows as <pending>. You need to use the NodePort assigned for the scdf-server service. You can use the following command to look up the URL to use `minikube service --url scdf-server`

## Codeless-backend

### codeless-backend database
#### `kubectl create -f kubernetes/backend-mysql/`
###### You can use `kubectl get all -l app=backend-mysql` to verify that the deployment, pod, and service resources are running.
###### You can use `kubectl delete all,pvc,secrets -l app=backend-mysql` to clean up afterwards.
###### If you run codeless-backend application locally, you can connect to this database `kubectl port-forward backend-mysql-{POD_ID} 3306:3306`

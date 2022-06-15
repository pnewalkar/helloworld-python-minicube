# helloworld-python-minicube
hello world python application with minikibe

Build and Run Docker Container
Install Docker Desktop
To build the image locally do the following.
docker build -t my_hello_world_final:latest .

To verify container run 
docker image ls

To run do the following: 
docker run -p 8080:8080 my_hello_world_final

Stop the running docker container by using control-c command

Running Kubernetes On MiniKube
Verify Kubernetes is working via minicube context

parag@Parag ~ % kubectl get nodes
NAME       STATUS   ROLES                  AGE    VERSION
minikube   Ready    control-plane,master   3d4h   v1.23.3

First save your docker image and load it on minikube:
. sudo docker save flask-change | bzip2 > flask-change.bz2
. sudo scp -i $(minikube ssh-key) flask-change.bz2 docker@$(minikube ip):/home/docker/flask-change.bz2
. minikube ssh
. docker load -i flask-change.bz2 

then apply the deployment on minikube:
kubectl apply -f deploy-kubetemp.yaml  

Verify the container is running
parag@Parag WORK_REPO % kubectl get pods                                   
NAME                            READY   STATUS    RESTARTS   AGE
hello-python-55644857c6-csgzw   1/1     Running   0          2m2s
hello-python-55644857c6-pql4h   1/1     Running   0          2m2s

Describe the load balanced service
parag@Parag WORK_REPO % kubectl describe services hello-flask-change-service
Name:                     hello-flask-change-service
Namespace:                hello-python
Labels:                   <none>
Annotations:              <none>
Selector:                 app=hello-python
Type:                     LoadBalancer
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       10.99.148.212
IPs:                      10.99.148.212
Port:                     <unset>  8080/TCP
TargetPort:               8080/TCP
NodePort:                 <unset>  31000/TCP
Endpoints:                172.17.0.4:8080,172.17.0.5:8080
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>





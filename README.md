# Docker dotnet core multiple projects solution example

Example .NET Core solution with docker image build from project referencing other projects.
Dockerfile and other configuration written according to [SoftwareDeveloper.Blog post with Docker introduction](https://www.softwaredeveloper.blog/multi-project-dotnet-core-solution-in-docker-image).

Feel free to ask a question using issue, create a pull request with enhancements and star repository if you find it helpful :)

## Building image

From root directory (where solution file -  _Docker-dotnet-core-multi-project-solution.sln_ is stored) run _Docker build_ command:

``` bash
docker build -f Aspnetcoreapp/Dockerfile -t aspnetcoreapp .
```

## Running container

To run container for the first time, type _Docker run_ command:

``` bash
docker run -d -p 8080:80 --name my-running-application aspnetcoreapp
```

## Stopping container

To stop running container run _Docker stop_ command:

``` bash
docker stop my-running-application
```

## Starting stopped container

To start container which was stopped, type _Docker start_ command:

``` bash
docker start my-running-application
```

## Navigate to Solution folder and run the below command

``` bash
docker build -f Aspnetcoreapp\Dockerfile -t docker-multi-project:V1 .
```

``` bash
docker run -d -p 8081:80 --name docker-multi-project-container docker-multi-project:V1
```

``` bash
docker stop docker-multi-project-container
```

``` bash
docker start docker-multi-project-container
```

``` bash
Browse the URL which is hosted http://localhost:8081/
```

## To view list of Docker image

``` bash
docker images
```

## To remove the image forcefully

``` bash
docker image rm -f <Image_Id>
```

## To Delete the Docker image from local store

``` bash
docker rmi <Image_Id>
```

## To Delete the Docker Image which is used by Stopped Container

``` bash
docker rmi -f <Image_Id>
```

## To Inspect the Docker Image

``` bash
docker inspect <Image_Name>:<Tag_Name>
```

## To view running containers

``` bash
docker ps
```

## To view all containers

``` bash
docker ps -a
```

## To Start the container

``` bash
docker start <Container_Name>
```

## To Kill the running container forcefully

``` bash
docker kill <Container_Id>
```

## To kill the container properly

``` bash
docker stop <Container_Name>
```

## To Pull the image and run the container

```bash
docker run <Image_Name>:<Tag_Name>
```

## To Pull the image and run the container with specific Port Binding

```bash
docker run -p <Host_Port>:<Container_Port> <Image_Name>:<Tag_Name>
```

## To Create the Container with specific Container Name

```bash
docker run -p <Host_Port>:<Container_Port> --name <Container_Name> <Image_Name>:<Tag_Name>
```

## To Pull the image

```bash
docker pull <Image_Name>:<Tag_Name>
```

## To login to Docker Hub

``` bash
docker login
```

## To Tag the local docker image to docker hub repo

``` bash
docker tag <Image_Name>:<Tag_Name> <Docker_User_Id>/<Repository_Name>:<Tag_Name>
```

## To Push Docker Image to Docker Hub in the specific repository

``` bash
docker push <Docker_User_Id>/<Repository_Name>:<Tag_Name>
```

## To Create a container from docker image

``` bash
docker create –name <Container_Name> <Image_Name>:<Tag_Name>
```

## To remove all the container that are not in a running state

``` bash
docker rm $(docker ps -a -q)
```

## To remove container

``` bash
docker rm -f <Container_Id>
```

## Edit the Container Contents

``` bash
https://jhooq.com/docker-edit-file-inside-container
```

## Step 1 : Get the Container Id

``` bash
docker ps -a
```

## Step 2 : Login inside the docker comtainer using Container Id using Root User (-u 0)

``` bash
docker exec -u 0 -it <Container_Id> /bin/sh
```

## Step 3 : Update the Package

``` bash
apt-get update
```

## Step 4 : Install "vim" editor and "nano" editor

``` bash
apt-get install vim
```

## Incase to restore the packages from private of custom feed refer the below link to implement

``` bash
# https://www.programmingwithwolfgang.com/restore-nuget-inside-docker/
```

``` bash
# https://github.com/WolfgangOfner/MicroserviceDemo/blob/master/CustomerApi/CustomerApi/Dockerfile
```

``` bash
#https://github.com/WolfgangOfner/MicroserviceDemo/blob/master/CustomerApi/CustomerApi/nuget.config
```

## To get the list of Docker network

``` bash
docker network ls 
```

## To create a new network in Docker

``` bash
docker network create <Network_Name>
```

## Create and Run a container with specific Docker Network

``` bash
docker run -d -p <Host_Port>:<Container_Port> --network <Network_Name>
```

## Assign a Enviroment variable while creating the Container

"/" used to split the long command to multiline command

``` bash
docker run -d -p <Host_Port>:<Container_Port> --network <Network_Name> /
-e <Envt_Variable_Name_1>=<Value1> /
-e <Envt_Variable_Name_2>=<Value2> 
--name <Container_Name> /
<Image_Name>:<Tag_Name>
```

## To See the Container Logs

``` bash
docker logs <Container_Id>
```

## To see last log from the Container

``` bash
docker logs <Container_Id> | tail
```

## To stream the container logs (With out re-querying the container log and also can edit the logs like "------------------" to mark the last log)

``` bash
docker logs <Container_Id> -f
```

## Docker Compose YAML file Syantax

Note: Docker Compose will take care of creating the network for all the containers if YAML has responsibilty to create more than one Container (Same Network to all the Containers)

```bash
version: '3' #Docker Compose Version
services:
  ##Specify the Container Name
  MyFirstContainerName:
    image: imageName:Tag
    ports:
      - 8080:80 #<Host_Port>:<Container_Port>
    environment:
      - SomeEnvtKey1=SomeValue1 #<Environment_Key1>=<Environment_Value1>
      - SomeEnvtKey2=SomeValue2 #<Environment_Key2>=<Environment_Value2>
    volumes:
      - SomeVolumeName:<Container_Directory_Path> #/var/lib/mysql/data
    
  MySecondContainerName:
    depends_on:
      - MyFirstContainerName #Dependent Service / Container Name in case MySecondContainerName is depends on MyFirstContainerName
    image: imageName:Tag
    ports:
      - 8080:80 #<Host_Port>:<Container_Port>
    environment:
      - SomeEnvtKey1=SomeValue1 #<Environment_Key1>=<Environment_Value1>
      - SomeEnvtKey2=SomeValue2 #<Environment_Key2>=<Environment_Value2>
  volumes:
    SomeVolumeName:
        driver: local # To tell docker create a directory and mount to reference Volumes
```

## To run the Docker Compose file

Note:By default Docker Compose is installed as part of the Docker Installation'

``` bash
docker-compose -f <Docker_Compose_FileName.yaml> up -d
"up" refers to run the container
```

## To stop and removed the containers which got created through Docker Compose file

Note:The below commpand will stop and remove the containers and also Docker network

``` bash
docker-compose -f <Docker_Compose_FileName.yaml> down
```

## Docker Volumes are used for data persistence

Note: In case data are stored in the container, while stop and remove the container data(s) are gone. This is the use case to have Docker Volumes to store the data.

Basically isolating the data from the container to Host machine and the mount the path in to the container

## 3 Volume Type

``` bash
1. Host Volumes
docker run -v <Host_Machine_Directory_Path>:<Container_Directory_Path>
```

``` bash
2. Anonymous Volumes
docker run -v <Container_Directory_Path>
In this case Docker takes care of creating the directory and mount to the Container Directory
```

``` bash
3. Named Volumes (Preferred Volume Type in Production)
docker run -v <name>:<Container_Directory_Path>
"name" can be any valid name
In this reference the volume by name and mount to the Container Directory
```

## K8s

It is a Container Orchestration Tool, manages the Containers

## K8s Components

``` bash
* Pod
    - Smallest unit of K8s
    - Abstraction over container
    - Pod is meant to run one application container
    - Usually 1 application per Pod
    - Each pod gets its own IP Address (1 IP Address / Pod)
    - application is talk to each other through Pod Ip Address. In case Pod crashes, new pod will be recreated and its get new IP address. Due to this, we need to adjust the IP address every time. To handle this scenario, "Service and Ingress" are there.
* Service
    - Service holds the static / Permanent IP Address
    - Attached to the Pod
    - Life cycle of Pod and Service not connected
    - 2 Type of service
        > External Service - It Opens a communication from external sources. Since the Url will have Node IP address, port number and Http protcol which is not that friendly. Due to that, Ingress came into the picture to tackle this which uses http and user friendly domain name.
        > Internal Service - It Opens a communication only for inmternal services
    - Load Balancer
* Ingress
    - Request comes to Ingress component from External source and forwards to the application Service.


* Volumes
    - K8s does not manage the data persistance
    - For data store
    - In case of pod crashes or dies or retarted data would be gone. So to avoid that "Volumes" are helping
    - Volumes are attaches to the Physical Storage where Pod Node is running or Remote Machine it can be Cloud or Some other Machine basically out side of the K8s cluster
    

* Secret
    -Meant for Sensitibve Information like User Name or Password
    -Its store as base 64 format
    - Connect it to the Pod, Pod will take read the secret configuration from it
* ConfigMap
    - Meant for Non Sensitive information
    - Its store as plain texrt format
    - External configuration to out application. Usually application uses the database to store the data and the DB connection string ot End point URl will be configured in applications. The database connection strings or end point Url changes in case, then we need to rebuild the image after changes, Push the image to Repo, Redeploy everything. Its tedious and long process. To avoid this we use the "ConfigMap"
    - Connect it to the Pod, Pod will take read the configuration from it


* Deployment
    - This is for Stateless Apps
    - Abstraction over Pods
    - Its used to define a blue print pods. This is useful when any of the pod crashes or dies. Services redirect the request to different pod which is available in the replicaset where blueprint defines at the time of deployment.
    - In real time we dont create the Pods we will create the Deployment. Deployment will take care of creating the "n" number of pods
    - We can replicate only the application pods through deployments not the Database. Because, Database is stateful. To manage the database we need a special mechanism to have the replica which is "Statefulset"
* Statefulset
    - This is for Stateful Apps or Databases
    - Its very Tedious to configure in K8s cluster
    - Often DB is hosted outside of K8s Cluster

```

## K8s Architecture

``` bash
1. Worker Node
    - Each node has multiple pods on it
    - Different nodes are interact with each other through services which is sort of load balancer
    - 3 process should be installed on every node
        > Container Runtime - Ex. Docker Runtime
        > Kubelet 
            - Interacts with both Container and Node
            - Starts the pod with a containr inside
        > Kube Proxy
            - Forward the request
            - Its has a logic of Forwarding mechanism
            - Its intelligent enough to forward the request from application pod to Database pod in the same node
```

``` bash
2. Master Node
    - Managing processes are handled by Master Nodes
        > New Node added to Cluster
        > Schedule a Pod
        > Recreate Pod when Pod Crashes
    - Multiple master nodes
    - All the below process are load balanced
    - 4 Processes are running in Master Node
        > Api Server
            -To deploy new application to K8s Cluster client will intercat through this
            - Client will be interacted through Api Server. Client can be Kubelet (CLI), K8s Dashboard (UI), K8s API 
            - Cluster Gateway
            - Acts as a Gatekeeper for Authentication
        > Schedular
            - Api Server send the request to Schedular to schedule a Pod to one of the worker nodes.
            - Schdular in intellignt enough to which worker node the pod has to be schduled.
            - Schdular decides on which node new Pod  should be scheduled depends on how much resources is used, RAM
        > Controller Manager
            - Detects the Cluster state changes like Pod Crashes and recover to the K8s state
            - Contoller manager send a request to Schdular to create a new pod
        > etcd
            - Its Key value store of a Cluster state
            - Cluster brain
            - Cluster changes (New Pod created, crahses, Recreated, etc..,) get stored in Key value store
            - All the components works based on the etcd data.
            - Actual application data wont get stored in etcd.
```

## To see the version of  kubectl

```bash
kubectl version
```

## To get all the k8s components list

```bash
kubectl get all
```

## To get list of status of the nodes

```bash
kubectl get node
```

## To get list of pod

```bash
kubectl get pod
```

## To get list of services

```bash
kubectl get service
```

## To get list of endpoints

```bash
kubectl get endpoints
```

## To get list of deployment

```bash
kubectl get deployment
```

## To get list of replicaset

- Replicaset is managing the replicas of a pod

```bash
kubectl get replicaset
```

## To get list of secrets

```bash
kubectl get secret
```

## Kubectl Create Commands

```bash
kubectl create -h
```

## To create the deployment component

- Blueprint to createa pods
- Between deployment and pod there is another layer called "Replicaset"

```bash
kubectl create deployment <Deployment_Name> --image=<Docker_Image_Name>
Ex: kubectl create deployment nginx-deployment --image=nginx
```

## To edit the deployment directly

```bash
kubectl edit deployment <Deployment_Name>
Ex: kubectl edit deployment nginx-deployment
```

## Useful Debugging Commands for K8s

```bash
## To debug Pods
kubectl logs <Pod_Name>
Ex: kubectl logs nginx-deployment-6767546888-mlrkj

## To debug Pod with detailed information
kubectl describe pods <Pod_Name>
Ex: kubectl describe pods nginx-deployment-6767546888-mlrkj

## To debug Pod and see the files inside the pod
kubectl exec -it <Pod_Name> -- bin/bash
kubectl exec -it <Pod_Name> -- bin/sh
kubectl exec -it <Pod_Name> sh
Ex: kubectl exec -it nginx-deployment-6767546888-mlrkj sh
```

## To Delete the Pods

```bash
## To delete pods we need to delete the deployment
kubectl delete deployment <Deployment_Name>
```

## kubectl Apply Command

```bash
- kubectl apply command is used to work with configuration file for the components
- kubectl apply command knows that when to create and update the deployment
kubectl apply -f <FILE_NAME.yaml>
```

## kubectl delete Command

```bash
kubectl delete -f <FILE_NAME.yaml>
```

## Syntax of K8s Component Configuration yaml file

3 Parts
    *Metadata
    *Specification - Based on resource Attributes / properties will differ
    *Status - It will be added by K8s

Multiple documents can be kept in single yaml file with 3 dash seperation (---)

```bash
apiVersion: apps/v1
kind: Deployment
metadata:
  name: <Component_Name> #nginx-deployment
  labels:
    app: <Name> #nginx - it can be anything but it should be referred to service if any
spec:
  replicas: <Replicas_Count>
  selector:
    matchLabels:
      app: <Component_Name> #nginx - it can be anything but it should be referred to other matching labels
  template:
    metadata:
      labels:
        app: <Component_Name> #nginx - it can be anything but it should be referred to other matching labels
    spec:
      containers:
      - name: nginx
        image: nginx:1.16
        resources:
          limits:
            memory: "128Mi"
            cpu: "500m"
        ports:
        - containerPort: <Container_Port> #8080
```

```bash
apiVersion: v1
kind: Service
metadata:
  name: <Component_Name> #nginx-service  
spec:
  selector:
    app: <Deployment_Meta_Label_Name> #nginx
  ports:
    - protocol: <Protocol> #TCP
      port:  <Service_Port> #80
      targetPort: <Container_Port> #8080
```

## To check pod is using the service

```bash
kubectl desc pods -o wide # This wwill return the IP Address

kubectl desc service # This will have Endpoint details where Pods IP address are mapped
```

## To see the status in the yaml file

```bash
kubectl get deployment <Deployment_Name> -o yaml
```

## To store the current deployment status in local machine

```bash
kubectl get deployment <Deployment_Name> -o yaml > <File_Name>.yaml
```

## To add a service of Type "Load Balancer" for External IP

```bash
Add type as "LoadBalancer" in the Service Kind and Add nodePort for external access which range from 30000 to 32767
```

## Namespace

```bash
- Namespace is virtual cluster in K8s cluster.
- By default it has 4 Namespaces
  *kube-system
    - Custom / User components should not be created under this. 
    - Its meant for System processes like Master node and kubectl process
  *kube-public
    - Publically access data
    - A Configmap which cointains cluster information data even w/o authentication
      kubectl cluster-info
  *kube-node-lease
    - Holds information about hearbeat of nodes
    - Determines the availability of node
    - Each node has associated lease Object in Namespace
  *default
    - Resources will be created under this when we create any components
```

## To create a Custom Namespace

```bash
- The need of custom Namespace is to have a logical grouping of resources inside a cluster

- Incase the 2 different teams are having same deployment name with 2 different set of configuration then latest one will overrice the other one. So, always good to have a namesapce while creating the resource

- Reuse the common shared Resources or components if we group it for different environment

- Access and Limits on Resources on Namespace

- To use the components (Secret, Configmap,etc..) which is located in other namespace we can use namespace.servicename as reference
  Ex: <Service_Name>.<Namespace_Name>
- Volume and node can not create inside the namespace. It lives globally in the cluster
  Try with below commands to find which all components are not bound to namespaces
  kubectl api-resources --namespaced=false

- Below command helps to determin which all components must have namespaces
  kubectl api-resources --namespaced=true

- While creating any components which supports namespace if not provided it will belong to "default" namespace

1. Through CLI Command
kubectl create namespace my-namespace

2. Through Configuration file in the meta property (Proper and recommented approach)
metadata:
  namespace: my-namespace
  .
  .

3. Can attach the namespace through cli itself
  kubectl apply -f <FileName>.yaml --namespace my-namespace  
```

## How to change the default namespace

Need to install the tool called "kubens". 
And ensure that all the kubens command will work with "Windows Power Shell"

Ensure that you have chocolately package installed
if not run the below commands in Windows Power Shell in Administrator mode
(Kubens install step by step) [https://community.chocolatey.org/packages/kubens]

```bash
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))

```

```bash
choco install kubens
```

The below commands provide the list of namespace and default namespace will be highlighted

```bash
kubens
```

To changes the default namespace to custom namespace which is already created

```bash
kubens <Other_Namespace_Name>
```

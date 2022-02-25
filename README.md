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

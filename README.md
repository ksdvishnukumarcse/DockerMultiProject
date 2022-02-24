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
https://jhooq.com/docker-edit-file-inside-container/#:~:text=How%20to%20edit%20file%20within%20Docker%20container%20or,vi%2C%20nano%2C%20vim%20etc.%20...%20More%20items...%20
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
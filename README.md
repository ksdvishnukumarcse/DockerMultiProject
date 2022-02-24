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
# docker build -f Aspnetcoreapp\Dockerfile -t docker-multi-project:V1 .
# docker run -d -p 8081:80 --name docker-multi-project-container docker-multi-project:V1
# docker stop docker-multi-project-container
# docker start docker-multi-project-container
# Browse the URL which is hosted http://localhost:8081/

# To view list of Docker image
# docker images

# To remove the image forcefully
# docker image rm -f <Image_Id>

# To Delete the Docker image from local store
# docker rmi <Image_Id>

# To Delete the Docker Image which is used by Stopped Container
# docker rmi -f <Image_Id>

# To Inspect the Docker Image
# docker inspect <Image_Name>:<Tag_Name>

# To view running containers
# docker ps

# To view all containers
# docker ps -a

# To Start the container
# # docker start <Container_Name>

# To Kill the running container forcefully
# docker kill <Container_Id>

# To kill the container properly
# # docker stop <Container_Name>

# To login to Docker Hub
# docker login

# To Tag the local docker image to docker hub repo
# docker tag <Image_Name>:<Tag_Name> <Docker_User_Id>/<Repository_Name>:<Tag_Name>

# To Push Docker Image to Docker Hub in the specific repository
# docker push <Docker_User_Id>/<Repository_Name>:<Tag_Name>

# To Create a container from docker image
# docker create –name <Container_Name> <Image_Name>:<Tag_Name>

# To remove all the container that are not in a running state
# docker rm $(docker ps -a -q)

# To remove container
# docker rm -f <Container_Id>

# Edit the Container Contents
# https://jhooq.com/docker-edit-file-inside-container/#:~:text=How%20to%20edit%20file%20within%20Docker%20container%20or,vi%2C%20nano%2C%20vim%20etc.%20...%20More%20items...%20
# Step 1 : Get the Container Id
# docker ps -a
# Step 2 : Login inside the docker comtainer using Container Id using Root User (-u 0)
# docker exec -u 0 -it <Container_Id> /bin/sh
# Step 3 : Update the Package
# apt-get update
# Step 4 : Install "vim" editor and "nano" editor
# apt-get install vim


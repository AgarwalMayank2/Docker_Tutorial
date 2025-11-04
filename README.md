# Docker_Tutorial

The given docker is a Linux kernel based.  
To install docker, we will use convenience script to install pre-releases of Docker on Linux. It is equal to the script at get.docker.com. For this run the following commands on terminal  
`curl -fsSL https://test.docker.com -o test-docker.sh`  
`sudo sh test-docker.sh`  

## Basic Docker Commands:-  
To run a docker image we run the command  
`docker pull <image_name>`  
If the image is present on the local system then it runs that docker image else it downloads the image from docker hub.  
To see all the docker images:- `docker images`  
To run a docker image:- `docker run <image_name>`  
`docker run -it <image_name>` by the '-it' (interactive) tag, we will be able to move into the container terminal which in this case can be an image of ubuntu.  
To see all the running docker containers:- `docker ps`  
To see all the running and exited containers:- `docker ps -a`  

To remove a docker image:- `docker rmi <image_name>` but for this, first the container of that image needs to be removed by:- `docker rm <container_name>`. container_name is basically the container_id which we can view from 'docker ps -a' command.  
To pull image of a specific version:- `docker pull <image_name>:<version>`  

To run a docker image in detach mode:- `docker run -d <image_name>`  
Detach mode means that now the image will run in background and we will not be able to see any inputs or interact with the container. By default, containers run in attach mode. We use '-d' tag to detach.  

For port binding:- `docker run -p<local_pc_port>:<container_port> <image_name>`  
When we run the docker ps -a command, we see some ports for each container. That is basically the port of the container at which data is received and sent. Remember it is not the port of our local computer. We can assign one port of our local computer to only one container. So we have to use multiple ports of our local computer to bind with multiple containers.  

To access logs of a container:- `docker logs <container_id>`  
To enter the bash or shell of a container for running some extra commands, we can run:- `docker exec -it <container_id> /bin/bash` or `docker exec -it <container_id> /bin/sh`.  

Sometimes we want that our containers should be able to talk among themselves without using any port. For this we can make a docker network which is made by:- `docker network create <network_name>`. To see all the networks running:- `docker network ls` and while running a docker image, use the tag `--network <network_name>`.

Docker compose:- It is a .yaml type file in which we write all the commands which we read previously and rather than executing those commands, we can execute this file. (Just make things easier)  

## Building docker image

To build our own docker, we make a 'Dockerfile' which is script which consists of instructions that how do we want to execute our files and with what dependencies. A dockerfile contains the following instructions:-  

`FROM` <base_image>  (The base image on which our files will be working let's say python 3.11)  
`WORKDIR` <directory> (The directory which contains the files)  
`RUN` <install_dependencies> (Installing all the dependies for our app)  
`COPY` <source_code> (Copying the source code of project)  
`CMD` <run_command>  (It will contain the command we will execute to finally run the project)  
`EXPOSE` <port>      (To expose ports of an image)  
`ENV` <variables>    (To define environment variables)  

After this, to make a build of this dockerfile, run the command:- `docker build -t <image_name>:<any_tag_version> .`  
Put '.' in last if you are in the same directory where your docker file is else give location.  

We can also attach our host memory with docker data so that our data is not lost after exiting the docker container. This is referred by docker volumes.  

## Push to docker hub  
We can push this docker iamge on the docker hub. For this, make a user on docker hub and while building the image build it as:- `docker build -t <username>/<image_name>:<tag> .`. Note that username is compulsory here and username is the name of our docker hub profile.  
Now run the command:- `docker push <username>/<image_name>:<tag>`.
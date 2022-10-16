# Building the base Image

## Basic image production includes content

The tomcat7 and jdk8 are used here. 

After downloading the tar package, unzip it.

**PS:** This is for the project war package. If you use the project jar package, you can remove tomcat

![Basic image production includes content](../Material/image/Project%20containerization%20transformation%20(4)%20—%20Basic%20image%20production%20includes%20content.png)

## Dockerfile

Dockerfile is a text file that contains instructions, each instruction builds a layer, so the content of each instruction is to describe how the layer should be constructed.

With Dockerfile, when we need to customize our own additional requirements, we only need to add or modify instructions on the Dockerfile to regenerate the image, saving the trouble of typing commands.

### File formating

![File formating](../Material/image/Project%20containerization%20transformation%20(4)%20—%20File%20formating.png)


**Dockerfile is divided into four parts:** 
1. basic image information
2. maintainer information
3. image operation instructions
4. container startup execution instructions.

At the beginning, the name of the image on which it is based must be specified, and then the maintainer information will generally be specified.

Followed by the mirror operation instructions, such as the RUN instruction.

Each time a RUN instruction is executed, a new layer is added to the image and submitted

Finally, there is the CMD command to specify the operation command when running the container.

### Detailed command

![File formating](../Material/image/Project%20containerization%20transformation%20(4)%20—%20command%20detail.png)

### Docker common commands

```shell script
Docker service start, stop, restart: service docker start(stop restart)
Show docker images: docker images
Delete docker image: docker rmi -f [image id]
Show running containers: docker ps
Show all containers: docker ps –a
Stop the container: docker stop [containerId]
Delete container: docker rm [containerId]
Start the container: docker start [containerId]
Download the image: docker pull
Image tagging: docker tag Current image name: TAG Warehouse address/image name: TAG
Image upload warehouse: docker push warehouse address/image name: TAG
Enter the container: docker exec -it [containerId] /bin/sh
Execute command: docker exec [containerId] -it [command]
Container console logs: docker logs -f [containerId]
Copy the file to the container: docker cp /directory/filename Container ID: container directory
Copy the container file to the local: docker cp container ID: file path local path
```

## Make a base image

### Write Dockerfile

#### Create dockerfile
```shell script
touch Dockerfile
```

#### Edit dockerfile
```shell script
#Introduce the virtual system as the underlying image
FROM centos:7
#author
MAINTAINER kris
#create date
ENV REFRESHED_AT 2019-01-13
#set time zone
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
#Handling encoding issues
ENV LANG C.UTF-8
#RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8
```









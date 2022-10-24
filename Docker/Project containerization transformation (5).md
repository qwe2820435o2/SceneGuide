# Jenkins packaged project image

## Server Planning

**192.168.92.137   Jenkins**
**192.168.92.139   Harbor**

**PS:** Both machines here need to install docker. For the specific installation tutorial, please refer to my previous article

## Contents required for packaging images

![20mertial detail](../Material/image/Project%20containerization%20transformation%20(5)%20—%20mertial%20detail.png)

### catalina.sh file

The tomcat memory is set in catalina.sh, packaged into the mirrored tomcat, and the memory size is limited for parameter tuning.

### demo-0.0.1-SNAPSHOT.war

Project war package, used for test packaging

### Dockerfile file

```shell script
# Based on the base image made earlier
FROM base:1.0
# author
MAINTAINER Travis
# log
ENV REFRESHED_AT 2019-01-13

# Copy the external configuration file to tomcat (different projects have different tomcat configurations, so this configuration is separate)
ADD catalina.sh  /usr/testimage/tomcat/bin/catalina.sh

# Switch the directory of the mirror and enter the /usr/testimage/tomcat/webapps directory
WORKDIR /usr/testimage/tomcat/webapps

# Create a directory under /usr/testimage/tomcat/webapps to store the war package of the web project
RUN mkdir demo-0.0.1-SNAPSHOT

# Copy the war to the directory
ADD demo-0.0.1-SNAPSHOT.war  /usr/testimage/tomcat/webapps/demo-0.0.1-SNAPSHOT

# Switch the directory of the mirror and enter the /usr/testimage/tomcat/webapps directory
WORKDIR /usr//testimage/tomcat/webapps/demo-0.0.1-SNAPSHOT

# Unzip the war package and delete the war package
RUN jar -xvf demo-0.0.1-SNAPSHOT.war
RUN rm  -rf demo-0.0.1-SNAPSHOT.war

```

## Create a new api_image packaging task
**ps: The ssh plugin is required here. The plugin has requirements for the jenkins version. If not, please upgrade the jenkins version**

### Log in to the Harbor warehouse on the machine where Jenkins is deployed

Authentication is required before pushing images to the repository

Enter account and password

```shell script
docker login 192.168.92.139
```

### Configure SSH hosts

ssh settings in system management - system configuration

![Configure SSH hosts](../Material/image/Project%20containerization%20transformation%20(5)%20—%20Configure%20SSH%20hosts.png)

### Set discard old builds with parameterized builds

![Set discard old builds with parameterized builds](../Material/image/Project%20containerization%20transformation%20(5)%20—Set%20discard%20old%20builds%20with%20parameterized%20builds.png)

### Configure the ssh packaging script

![Configure the ssh packaging script](../Material/image/Project%20containerization%20transformation%20(5)%20—Configure%20the%20ssh%20packaging%20script.png)

```shell script
DATE=`date +%Y%m%d%H%M%S`
cd /usr/local/testjar/${IMAGE_NAME}
docker build --no-cache -t ${IMAGE_NAME}:$DATE .
sleep 1
docker tag ${IMAGE_NAME}:$DATE 192.168.92.139/library/${IMAGE_NAME}:$DATE
docker push 192.168.92.139/library/${IMAGE_NAME}:$DATE
sleep 1
docker rmi ${IMAGE_NAME}:$DATE
sleep 1
docker rmi 192.168.92.139/library/${IMAGE_NAME}:$DATE
```

### Package test

![Package test](../Material/image/Project%20containerization%20transformation%20(5)%20—%20Package%20test.png)

### View logs in Console Output













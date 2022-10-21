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
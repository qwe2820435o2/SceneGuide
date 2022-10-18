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
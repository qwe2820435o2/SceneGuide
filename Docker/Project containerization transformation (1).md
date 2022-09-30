# Deploy Jenkins continuous integration server

## Overall process

1. Jenkins builds jars based on build parameters ——> Jenkins pulls code from github ——> 
Maven into a jar package ——> Copy the jar to the specified directory according to the build parameters

2. Mirror build based on build parameters on Jenkins ——> Jenkins packages images according to Dockerfile ——> 
Push to Harbor, an enterprise-level private repository ——> Delete locally generated images

3. Humpback lightweight container management tool ——> Pull the image from the repository ——> Deploy containers for each host

## Install Jenkins
**address:** https://jenkins.io/

### Download the Jenkins package from the official website

1. Put jenkins.war in /usr/local

2. Execute nohup java -jar httpPort=8080 jenkins.war & to start the jenkins server

3. Access IP+8080 port to see

![Download Jenkins](../Material/image/Project%20containerization%20transformation%20(1)%20—%20download%20jenkins%20.png)

### View password

```shell script
cat /root/.jenkins/secrets/initialAdminPassword
```

### Install recommended plugins

![Install plugins](../Material/image/Project%20containerization%20transformation%20(1)%20—%20install%20plugin%20.png)

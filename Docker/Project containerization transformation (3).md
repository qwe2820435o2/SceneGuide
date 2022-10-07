# Enterprise-level private warehouse Harbor deployment

## Docker engine installation

### Remove old versions of Docker
```shell script
sudo yum remove docker \
	                  docker-client \
	                  docker-client-latest \
	                  docker-common \
	                  docker-latest \
	                  docker-latest-logrotate \
	                  docker-logrotate \
	                  docker-selinux \
	                  docker-engine-selinux \
	                  docker-engine
```

### Install the latest version

```shell script
sudo yum install -y yum-utils \ device-mapper-persistent-data \ lvm2
sudo yum-config-manager \ --add-repo \ https://download.docker.com/linux/centos/docker-ce.repo
sudo yum install docker-ce
```

### Start Docker
```shell script
sudo systemctl start docker
```

### Set startup
```shell script
systemctl daemon-reload
systemctl restart docker
```

### Test if the installation is successful
```shell script
docker run hello-world
```

![Test if the installation is successful](../Material/image/Project%20containerization%20transformation%20(3)%20—%20Test%20if%20the%20installation%20is%20successful.png)

















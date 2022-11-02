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

## Docker Compose installation

### Install the latest version

```shell script
sudo curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

### Setting permissions

```shell script
sudo chmod +x /usr/local/bin/docker-compose
```

### Test if the installation is successful
```shell script
docker-compose --version
```
![Test if the installation is successful](../Material/image/Project%20containerization%20transformation%20(3)%20—%20test%20docker-compose%20install.png)

## Install Harbor

### Get the package address

**Version package address:** https://github.com/goharbor/harbor/releases

![Version package address](../Material/image/Project%20containerization%20transformation%20(3)%20—%20harbor%20address.png)


### Download

```shell script
wget https://storage.googleapis.com/harbor-releases/release-1.7.0/harbor-online-installer-v1.7.1.tgz
```

### Decompress
```shell script
tar -zxvf harbor-online-installer-v1.7.1.tgz
```

### Change setting
```shell script
vim harbor.cfg
```

**Modify the hostname to the ip of the machine:**

![Change harbor ip](../Material/image/Project%20containerization%20transformation%20(3)%20—%20Change%20harbor%20ip.png)


### Install
```shell script
./install.sh
```

### Test if the installation is successful

Access the host ip, jump to this page, the installation is successful

![test harbor install](../Material/image/Project%20containerization%20transformation%20(3)%20—%20test%20harbor%20install.png)

## Push and pull images

### Configure the repository for the http protocol

Docker's default repository address is https protocol, but harbor repository defaults to http protocol.

If you need to use the http protocol warehouse, you need to make the following settings in the /etc/docker/daemon.json configuration file of docker:

```json
{
  "registry-mirrors": ["https://th3wopsw.mirror.aliyuncs.com"],
  "insecure-registries": ["192.168.92.139"]
}
```

### Login

Enter account and password

```shell script
docker login 192.168.92.139
```

### Making Tag

Just use our previous hello-world image for testing

```shell script
docker tag hello-world 192.168.92.139/library/hello-world
```

### Pushing image

```shell script
docker push 192.168.92.139/library/hello-world
```

![Push image](../Material/image/Project%20containerization%20transformation%20(3)%20—%20pushing%20image.png)

![Push image finish](../Material/image/Project%20containerization%20transformation%20(3)%20—%20pushing%20image%20finish.png)

### Pulling image

You can click to enter the mirror warehouse, copy the pull statement, and execute

```shell script
docker pull 192.168.92.139/library/hello-world:latest
```

![Pulling image](../Material/image/Project%20containerization%20transformation%20(3)%20—%20pulling%20image.png)


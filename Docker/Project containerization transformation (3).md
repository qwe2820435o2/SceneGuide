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


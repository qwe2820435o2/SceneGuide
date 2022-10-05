# Jenkins packages project jar package

## Install Maven

### Download Maven

```shell script
cd /usr/local
wget http://mirror.bit.edu.cn/apache/maven/maven-3/3.5.0/binaries/apache-maven-3.5.0-bin.tar.gz
```

### decompress

```shell script
tar -zxvf apache-maven-3.5.0-bin.tar.gz
```

### Set MAVEN_HOME

1. vim /etc/profile
2. Configure the Maven installation path to MAVEN_HOME
```shell script
export MAVEN_HOME=/usr/local/maven
export PATH=$PATH:$MAVEN_HOME/bin
```
3. Effective immediately after modification
```shell script
source /etc/profile
```

## Install Git

### Install gcc

```shell script
yum install gcc
```

### Install g++
```shell script
yum install gcc-c++
```

### Install the required packages for compilation

```shell script
yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel
yum install gcc perl-ExtUtils-MakeMaker
```

### Download the installation package
```shell script
wget -P /usr/local/git-2.12.2 https://www.kernel.org/pub/software/scm/git/git-2.12.2.tar.gz
```

### Unzip the source package
```shell script
tar zxvf git-2.12.2.tar.gz
```

### Compile and install
```shell script
cd git-2.12.2/
./configure --prefix=/usr/local/git-2.12.2 && make install
```

### Configure Git_HOME
```shell script
1. vim /etc/profile
2. Configure the Git installation path as Git_HOME
   export Git_HOME=/usr/local/git-2.12.2
   export PATH=$PATH:$Git_HOME/bin
3. Effective immediately after modification
   source /etc/profile
4. Check git version
   git --version
```

## Install the publish over ssh plugin
### Find the plugin in optional plugins
![publish over ssh plugin](../Material/image/Project%20containerization%20transformation%20(2)%20—%20publish%20over%20ssh%20plugin.png)

### After checking it, click Install directly
![Install plugin](../Material/image/Project%20containerization%20transformation%20(2)%20—%20install%20plugin.png)

## Configure SSH Server
1. Click System Management - System Settings
2. Scroll down to find publish over ssh, where Passphrase is the password of the 137 machine
```properties
Name is the name

Hostname is the machine ip

Username is the account

Remote Directory is the directory accessible by jenkins
```
![Configure SSH Server](../Material/image/Project%20containerization%20transformation%20(2)%20—%20Configure%20SSH%20Server.png)

## Configure packaging tasks

### Create free-style software projects

![Create free-style software projects](../Material/image/Project%20containerization%20transformation%20(2)%20—%20Create%20free-style%20software%20projects.png)

### Take the project on github as an example

![Take the project on github as an example](../Material/image/Project%20containerization%20transformation%20(2)%20—%20Take%20the%20project%20on%20github%20as%20an%20example.png)

### Configure the project address
1. Check the Github project and fill in the project address
2. Click to discard old builds, set the number of days to save the build, and the maximum number of builds
![Configure the project address](../Material/image/Project%20containerization%20transformation%20(2)%20—%20Configure%20the%20project%20address.png)

### Configure build parameters

Project name, path to place the jar package
![Configure the project address](../Material/image/Project%20containerization%20transformation%20(2)%20—%20Configure%20build%20parameters.png)

### Configure source code management


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














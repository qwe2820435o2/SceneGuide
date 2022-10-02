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









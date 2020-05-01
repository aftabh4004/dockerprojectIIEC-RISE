# Docker and JDBC

This is my project for Docker training, it will do Database Connectivity to Java. This can be used for educational purpose because usually new guys to Java find difficult to do Java database connectivity.

I used Docker Compose to launch two container one for database and other for devlopment of java code

## Environment used for devlopment of project
1. OS : Ubuntu 18.04.4 LTS
2. Docker : Docker version 19.03.8, build afacb8b7f0
3. Docker Compose : docker-compose version 1.23.1, build b02f1306

## Initial image used
[mysql:latest](https://hub.docker.com/_/mysql)

[centOS:latest](https://hub.docker.com/_/centos)

## Configuring the initial centOS image

After pulling centOS latest image we have to install listed software using yum install
1. openjdk-1.8 (this will install jre)
2. default-jdk (this will install jdk)
3. vim
4. unzip
Download which is mandatory for doing Java Database connectivity.
Go to root and type
..shell script
wget https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-8.0.20.zip
unzip mysql-connector-java-8.0.20.zip
..
Inside the unzip dir you have mysql-connector.
### Append .bashrc file
... 


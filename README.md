# Docker and JDBC

This is my project for Docker training, it will do Database Connectivity to Java. This can be used for educational purpose because usually, new guys to Java find difficult to do Java database connectivity.

I used Docker Compose to launch two containers one for database and other for the development of java code

## Environment used for development of the project
1. OS: Ubuntu 18.04.4 LTS
2. Docker : Docker version 19.03.8, build afacb8b7f0
3. Docker Compose : docker-compose version 1.23.1, build b02f1306

## Initial image used
[mysql:latest](https://hub.docker.com/_/mysql)

[centOS:latest](https://hub.docker.com/_/centos)

## Configuring the initial centOS image

First of all get your root terminal. Then pull images

```shell
docker pull centOS:latest
docker pull mysql:latest
```


After pulling centOS latest image we have to install listed software using yum install
1. openjdk-1.8 (this will install jre)
2. default-jdk (this will install jdk)
3. vim
4. unzip

Download mysql-connector which is mandatory for doing Java Database connectivity.
Go to root and type

```shell
wget https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-8.0.20.zip
unzip mysql-connector-java-8.0.20.zip
```

Inside the unzip dir you will have mysql-connector.

Go to home directory , .bashrc file is there


```shell
cd ~
vim .bashrc
```

### Append .bashrc file

```bash
export CLASSPATH=path/to/mysql-connector
```
Now, Create a simple Template in java language which opens up for the user which do initial steps on Database connectivity

```java
import java.sql.*;
public class MysqlCon{
        //change the class name same as your file name
        public static void main(String args[]){
                try{
                        Class.forName("com.mysql.cj.jdbc.Driver");
                        Connection con=DriverManager.getConnection("jdbc:mysql://dbos:3306/mydb","aftab","ubuntu");
                        //here mydb is database name, root is username and password  
                        
                        //your code goes here
                        
                        /*
                         *Sample Code
                         *
                         *
                        Statement stmt=con.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE,ResultSet.CONCUR_READ_ONLY);
                        ResultSet rs=stmt.executeQuery("select * from employee");
                        rs.first();
                        System.out.println("ID\tName");
                        while(rs.next()){
                                System.out.println(rs.getInt(1) + "\t" + rs.getString(2));
                        }
                        */

                        con.close();
                }catch(Exception e){ System.out.println(e);}
        }
}

```

Before you uncomment and rum this code for testing make sure the table is there in the database otherwise you will get SQLException.
To make things easier for the user let's create a shell script which copies the pre-created template to the dir where the docker volume is mounted with the name passed as an argument  and open it up for editing

```shell
cp /root/MysqlCon.java /home/program/$1;
cd /home/program;
vim /home/program/$1;
```

We can make an alias do make things more convenient

Again do,

```shell
cd ~
vim .bashrc
```

### Append .bashrc file

```bash
alias jtemp=". /yourscriptname.sh"
```

Everything is now configured, Commit the image with proper naming syntax (username/repo name) and upload the image to Docker hub.

```shell
docker commit [Container name:tagname] [New container name: tagname]
docker tag [New container name: tagname] [username/reponame:tagname]
docker login 
docker push [username/reponame:tagname]
```

Provide Credential if asked.
Link to my Custom image [click here](https://hub.docker.com/repository/docker/aftabh4004/centjava)

Or pull image by

```shell
docker pull aftabh4004/centjava
```

To launch containers by docker-compose file provided in this repo.

Go to the same dir where docker-compose.yml file is and do

```shell
docker-compose up
```

Both containers will be launch.

## Guide for the user

As soon as your container launch it start showing logs, 
Now open another root terminal and do 

```shell
docker ps -a
```

Note down the initial two or four character of container ID of the container named desktop_javatemplateos...
Attach it to get its bash terminal

```shell
docker attach [INITIAL CONTAINER ID]
```

Now to get the Template,

```shell
jtemp myfile.java
```
Give your file name in place of myfile.java

vim editor will be open, edit the code accordingly.


## Thank you



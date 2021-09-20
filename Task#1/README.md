# Spring Boot Hello World

A spring boot enabled hello world application

- Task#1.1 and 1.3
-   Deploy the application to Tomcat or use command-line to show its output (Non-containerized App)
-   Project is a real world Java project using Maven build, containerizing a maven project and showing the output
-   Executing as maven build with embedded tomcat application server
```
open maven sand box environmnet in Orelly, and follow below steps
git clone https://github.com/ngtrainings/HelloWorld/
cd HelloWorld/springboot-helloworld-master
mvn clean package
java -jar target/helloworld-0.0.1-SNAPSHOT.jar
open WebPreview at portno: 8080
```

- Task#1.2
- To run jar as docker application ( Containerized App) (assumption docker is installed on your machine)
```
git clone https://github.com/ngtrainings/HelloWorld/
cd HelloWorld/springboot-helloworld-master/
docker build -t ngtrainings/springboot-helloworld-master:v5 .
docker images
docker run -p80:8080 ngtrainings/springboot-helloworld-master:v5
open WebPreview at portno: 80
docker login
docker push ngtrainings/springboot-helloworld-master:v5
```

- Task#1.4
- To run this as a docker application with oracle jdk 
```
git clone https://github.com/ngtrainings/HelloWorld/
cd HelloWorld/springboot-helloworld-master/
create Dockerfile with below content

FROM store/oracle/serverjre:1.8.0_241-b07
COPY . /data/springboot-helloworld
WORKDIR /data/springboot-helloworld
EXPOSE 2020
CMD ["java", "-jar", "helloworld-0.0.1-SNAPSHOT.jar"]

login with docker id
docker build -t helloworld .
docker images
docker run -p80:2020 helloworld
open WebPreview at portno: 80
```

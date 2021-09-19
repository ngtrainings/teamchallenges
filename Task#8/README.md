
- CI CD Pipeline - local setup
```
Create new CI CD Pipeline for https://github.com/ngtrainings/teamchallenges.git
Submit new build
Verify v4 image in dockerhub
Test v4 code in local
```

- docker images publish to docker hub via Jenkins CI/CD pipelines
```
Click on https://www.katacoda.com/courses/docker/deploying-first-container
docker run -p 80:8080 -p 50001:50000 -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts-jdk11

or 

https://learning.oreilly.com/scenarios/jenkins-sandbox/9781098117825/

Configure Maven version
Jenkins install Maven for you
    You must go to Jenkins Global Tool Configuration, and configure a Maven version with automatic installer (from the web).
    In Job configuration, for Maven Version, you must select that particular version that you've just configured.

Add Maven-3.6.1 in global configuration

create new jenkins pipeline job

Create new build_simple_java pipeline https://github.com/ngtrainings/teamchallenges.git
prefix jenkinsfile name with teamchallenges/Task#5
Submit new build
Go to terminal and run jar file
cd /var/jenkins_home/workspace/jenkin-docker-integration/target/
java -jar HelloNextGen-0.0.1-SNAPSHOT.jar

```

- build_multi_branch_pipeline
```
Create new build_multi_branch_pipeline pipeline https://github.com/ngtrainings/HelloNextGen.git
Submit new build with params
Verify pipeline
```

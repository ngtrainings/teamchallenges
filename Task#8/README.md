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

https://github.com/ngtrainings/teamchallenges.git


```

- build_multi_branch_pipeline
```
Create new build_multi_branch_pipeline pipeline https://github.com/ngtrainings/HelloNextGen.git
Submit new build iwth params
Verify pipeline
```

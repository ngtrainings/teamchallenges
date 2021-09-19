
- CI CD Pipeline - local setup ( windows ), change bat to sh in Jenkinsfile to run it in unix env.
```
Create new CI CD Pipeline for https://github.com/ngtrainings/teamchallenges.git

Configure Maven version
Jenkins install Maven for you
    You must go to Jenkins Global Tool Configuration, and configure a Maven version with automatic installer (from the web).
    In Job configuration, for Maven Version, you must select that particular version that you've just configured.
    
Configure docker hub credentials - DOCKER_REGISTRY_CREDENTIALS
    You must go to Global credentials Configuration and configure DOCKER_REGISTRY_CREDENTIALS id with docker username/password

Prefix Jenkinsfile with Task#8
Submit new build
Check docker desktop for new version image
Check command line to verify deploymet success
Verify application url in browser

```

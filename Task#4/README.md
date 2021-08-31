- docker compose services for Mongo and Mongo-express images
```
git clone https://github.com/ngtrainings/teamchallenges.git
cd teamchallenges/Task#4
docker-compose mongo.yml up -d
docker ps
docker-compose mongo.yml down -d
```

- docker compose services for Mariadb, phpadmin and wordpress
- start and stop the WP site using docker-compose
```
git clone https://github.com/ngtrainings/teamchallenges.git
cd teamchallenges/Task#4
docker-compose maria-wp-php.yml up -d
docker ps
docker-compose maria-wp-php.yml down -d
```

- docker compose services for Mariadb, phpadmin and wordpress
- scale up/down the WP site using docker-compose
```
git clone https://github.com/ngtrainings/teamchallenges.git
cd teamchallenges/Task#4
docker-compose maria-wp-php.yml up -d --scale db=2 myadmin=2 wordpress=3
docker ps
docker-compose maria-wp-php.yml down -d
```

- Task#3
- Create a sample Wordpress site for my team using container so that we will understand how to containerised web application. Use MariaDB 10.4 as Database, PHPMyAdmin v5.1 as DB client and the latest version of Wordpress
- Use only Docker CLI commands executed on the command-line or via a shell script.
```
docker network create wp-network

docker run -d --name wordpress \
    --net wp-network \
    -p 80:8080 \
    -v wordpress:/var/www/html \
    -e WORDPRESS_DB_USER=admin \
    -e WORDPRESS_DB_PASSWORD=pass \
    wordpress

open WebPreview at portno: 80
```

- Task#3
- Create a sample Wordpress site for my team using container so that we will understand how to containerised web application. Use MariaDB 10.4 as Database, PHPMyAdmin v5.1 as DB client and the latest version of Wordpress
- Use only Docker CLI commands executed on the command-line or via a shell script.
```
docker network create wp-network

docker run -d --name=mariadb \
    --net wp-network \
    -v db_data:/var/lib/mysql \
    -e MYSQL_DATABASE=demodb \
    -e MYSQL_USER=admin \
    -e MYSQL_PASSWORD=pass \
    -e MYSQL_ALLOW_EMPTY_PASSWORD=no \
    -e MYSQL_RANDOM_ROOT_PASSWORD=pass \
    mariadb:10.4


docker run --name myadmin -d \
    --net wp-network \
    --link mariadb:db \
    -p 80:80 phpmyadmin/phpmyadmin
    
   
docker run -d --name=wordpress \
    --net wp-network \
    -p 80:80 \
    -v wordpress:/var/www/html \
    -v site_logs:/var/logs \
    -e WORDPRESS_DB_HOST=mariadb \
    -e WORDPRESS_DB_NAME=demodb \
    -e WORDPRESS_DB_USER=admin \
    -e WORDPRESS_DB_PASSWORD=pass \
    wordpress
  

open WebPreview at portno: 80
open WebPreview at portno: 81
```

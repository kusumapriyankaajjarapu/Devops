# Databases

## MySQL  

### Create a container instance
    docker run -d –name=mysqldb -e MYSQL_ROOT_PASSWORD=pwd$123 mysql
### Access the container
    docker exec -it mysqldb mysql -u root –p
### Using Dockerfile
    FROM ubuntu
    RUN apt-get update && apt-get install -y mysql-server
    CMD ["mysqld_safe"]
	
## POSTGRES

### Create a container instance
    docker run -d --name=postgressql -e POSTGRES_PASSWORD=pwd$123 postgres
### Access the container
    docker exec -it postgressql psql -U postgres
### Using Dockerfile
    FROM ubuntu
    RUN apt-get update && apt-get install -y postgresql postgresql-contrib
    CMD postgres
    
## MONGODB

### Create a container instance
    docker run --name=mongodb mongo
### Access the container
    docker exec –it mongodb mongosh
### Using DockerFile
    FROM ubuntu:bionic
    RUN apt-get update && apt-get install -y wget\
        && apt-get install -y gnupg
    RUN wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | apt-key add - \
        && echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/6.0 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-6.0.list \
        && apt-get update \
        && apt-get install -y mongodb
    RUN mkdir data -p /data/db\
        && chown `id -u` /data/db
    CMD mongod

# Servers

## Nginx

    docker run -d --name nginx_server -p 8080:80 -v E:/Priyanka/DEVOPS/Docker/nginx/:/usr/share/nginx/html  nginx
### Using DockerFile
    FROM ubuntu
    RUN apt-get update && apt-get install -y nginx
    COPY index.html /var/www/html
    CMD ["nginx", "-g", "daemon off;"]

## Apache

    docker run -d --name apache -p 8080:80 -v E:/Priyanka/DEVOPS/Docker/nginx/:/usr/local/apache2/htdocs/ httpd
### Using DockerFile
    FROM ubuntu
    RUN apt-get update && apt-get install -y apache2
    COPY index.html /var/www/html
    CMD apachectl -D FOREGROUND

 
 



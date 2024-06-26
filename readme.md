#DOCKER COMPOSE
On docker file you have two main components:
    - docker-compose.yml 
    - Dockerfile. 
    Use docker-compose to create different services you wish to use. In this case
Web (ngingx) and App (php).
Each service can use a predefined IMAGE from docker hub or can BUILD a custom Image.
```
services:
  web:
    image: nginx:latest
```
```
services:
  app:
    build: nginx:latest
```

#DOCKERFILE

in the Dockerfile you can use different commands to build image
https://docs.docker.com/reference/dockerfile/
RUN - execute build commands
```
RUN docker-php-ext-install pdo pdo_mysql
```


#DOCKER COMMANDS

##docker images - get informations about current docker images
```docker images ls```

##docker build
build image with flags:
 -t for tag 
 -f for file path
and  . for current folder 
```docker build -t cristiand:php81 -f php/Dockerfile .```

#CREATE VOLUME MAPPING
## create a volume to read from the nginx config file nginx/conf.d
``` 
    volumes:
        - ./nginx/conf.d/default.conf:/etc/nginx/conf.d/default.conf
```




#customize NGINX

default address of nginx config file /etc/nginx/conf.d/default.conf
create a file and folder structure to mirror this config path

#add composer
allow superuser setting an environment variable
```ENV COMPOSER_ALLOW_SUPERUSER=1```

create a multystage Dockerfile using COPY to copy the composer binaries
```COPY --from=composer:2.4 /usr/bin/composer /usr/bin/composer


#creating a docker dev 
#customizing dev file

remove the vendor folder because it's not required

#customizing prod file
The production will miss the volumes
- we don't need to expose the ports for the database
- move the environment to envirnonment variables
- remove the volumes
- create an nginx dockerfile for the production in the nginx folder




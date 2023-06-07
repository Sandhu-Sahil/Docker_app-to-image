# commands
Or use .yaml file directly

## create docker 
network docker network create mongo-network

## start mongodb 
docker run -d \
-p 27017:27017 \ 
-e MONGO_INITDB_ROOT_USERNAME=admin \
-e MONGO_INITDB_ROOT_PASSWORD=password \ 
--net mongo-network \
--name mongodb \
mongo

## start mongo-express
docker run -d \
-p 8081:8081 \
-e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
-e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
-e ME_CONFIG_MONGODB_SERVER=mongodb \
--net mongo-network \
--name mongo-express \
mongo-express

# Create image of your APP

Before creating image check that your image has right database link, for more info check server.js

### To build a docker image from the application
```
sudo docker build -t docker-first:1.0 .       
```
The dot "." at the end of the command denotes location of the Dockerfile.

# YAML File
first we have to write file manually and check weather the info of docker first in .yaml is imported from image created not from the aws docker repository
```
docker-first:
    image: docker-first:1.0
    ports:
    - 3000:3000
```

### run command
```
sudo docker-compose -f docker-compose.yaml up -d
```
```
sudo docker-compose -f docker-compose.yaml down
```

### Mongo
mongo express is up on:
```
http://localhost:8080/
```

# Push Image to DockerHub Repository
First create a DockerHub repository and use it's link to to push your image to the repository
<br>Also check docker login
```
sudo docker login
```

#### After creating repository create a tag and commit for the push
```
sudo docker tag docker-first:1.0 sandhu0sahil/sandhu:1.0
```
#### Now push the image to the repository
```
sudo docker push sandhu0sahil/sandhu:tagname
```

#### Now instead of creating your own image you can pull the image directly and run it without having the code of the whole program
```
sudo docker pull sandhu0sahil/sandhu:1.0
```

Also change this in .yaml file 
```
docker-first:
    image: sandhu0sahil/sandhu:1.0
    ports:
    - 3000:3000
```
after this you only need .yaml file to run the app not the whole source code
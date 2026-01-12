# ROBOSHOP PROJECT:
# mongodb:
* first we need to create database mongodb
* search for mongodb office docker image then use dockerfile we are using mongodb:version 7.0 so will take that version from docker repository
* Map a volume to /docker-entrypoint-initdb.d containing .sh or .js files, they will be executed in alphabetical order.
* docker logs <contaner_name> -> for showing logs of the container
* docker build -t mongodb:v1 .
* docker run -d --name mongodb mongodb:v1 
* docker ps
* docker exec -it mongodb bash
* mongosh -> to connect database inside the container
* show dbs -> show databases list
# catalogue:
* catalogue deploying the node js application and version is 20
* so we can take node:20 directly refer this image from docker repository.
* docker build -t catalogue:v1 .
* docker run -d --name catalogue catalogue:v1
* docker exec -it catalogue bash
* curl http://localhost:8080/health -> to check catalogue health and mongodb dependency
* here catalogue is true and mongodb dependency is false why?
# docker networking:
* docker has 3 networks
    - host network -> no need docker interface directly connect host
    - bridge network -> docker creates another network to inside the server and allowcates that ip address to containers.
    - none network
* docker default bridge network does'nt communicates to each other.
* so user your bridge network 
* create your own network interface
* docker network ls -> show all networks
* docker network --help -> show all network commands
* docker network create <network_name>
* docker network disconnect <type_of_network> <container_name> (type_of_network = bridge,host,none)
* disconnect with default bridge network to all containers and then connect the your own(roboshop) network for all containers.
* docker network connect <type_of_network> <container_name> (docker network connect roboshop mongodb)
# redis:
* directly run redis image without docker file
* docker run -d --name redis --network roboshop redis:7
# user:
* user also running the same node js application like catalogue then we use catalogue code but we need to chagne the environment variables as per documentation.
* use same roboshop network for user as well
* docker build -t user:v1 .
* docker run -d --network roboshop --name user user:v1
* docker exec -it user bash
* curl http://localhost:8080/health -> connected mongodb and app were true.
# mysql:
* create dockerfile for mysql
* docker build -t mysql:v1 .
* docker run -d --name mysql --network roboshop mysql:v1
* docker exec -it mysql bash
* inside the mysql for checking databases
* mysql -u root -pRoboshop@1 -> for database login
* show databases -> showing databases
* docker logs <contaner_name> -> for showing logs of the container
# shipping:
* create dockerfile for shipping
* we are using shipping 3.9.11
* docker build -t shipping:v1 .
* docker run -d --name shipping --netowork roboshop shipping:v1
* docker exec -it shipping bash
* curl http://localhost:8080
* in Dockerfile we copy entier folder of src like COPY src/ ./src
# rabbitmq:
* we directly run rabbitmq, why rabbitmq is no configuration and no dependencies
* we are taken rabbitmq versin is 3 rabbitmq:3



# ROBOSHOP PROJECT:
* first we need to create database mongodb
* search for mongodb office docker image then use dockerfile we are using mongodb:version 7.0 so will take that version from docker repository
* Map a volume to /docker-entrypoint-initdb.d containing .sh or .js files, they will be executed in alphabetical order.
* docker build -t mongodb:v1 .
* docker run -d --name mongodb mongodb:v1 
* docker ps
* docker exec -it mongodb bash
* mongosh -> to connect database inside the container
* show dbs -> show databases list

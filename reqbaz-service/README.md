# Requirements Bazaar Backend Service

This Dockerfile retrieves the latest version from the continuous integration server on runtime and serves the backend service on port 8080.

## Run from Docker Hub
The image is built automatically on Docker Hub:

https://registry.hub.docker.com/u/rwthacis/reqbaz-service/

To run it, simply call:

`docker run -d -p 8080:8080 -e MYSQL_HOST=host -e MYSQL_DATABASE=reqbaz -e MYSQL_USER=user -e MYSQL_PASSWORD=pass rwthacis/reqbaz-service`

Replace `host`, `reqbaz`, `user` and `pass` with your respective MySQL data. If you don't have a MySQL server at hand, try the one provided by the Learning Layers project. It consists of two parts, a data container that you can backup and the actual MySQL server container. Run these two lines to start it:

`docker run --name mysql-data learninglayers/mysql-data`

`docker run -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD=pass --volumes-from mysql-data --name mysql learninglayers/mysql`

Replace `pass` with a meaningful root password. To create a database and user that you can insert into the Requirement Bazaar's run command, run the following command:

`docker run --link mysql:mysql learninglayers/mysql-create -ppass --new-database reqbaz --new-user myuser`

Replace `pass` with the MySQL root password, `reqbaz` with the database name and `myuser` with the desired username. The command-like docker container will return a randomly generated password for this user. Finally, you may simply start the Requirements Bazaar like this:

`docker run -d -p 8080:8080 -e MYSQL_HOST=host -e MYSQL_DATABASE=reqbaz -e MYSQL_USER=user -e MYSQL_PASSWORD=pass --link mysql:mysql rwthacis/reqbaz-service`

## Build it on your own
Of course you can build the image yourself if you don't want to rely on Docker Hub:

1. `git clone https://github.com/rwth-acis/RequirementsBazaar-Dockerfiles.git`
2. `cd RequirementsBazaar-Dockerfiles/reqbaz-service`
3. `docker build -t rwthacis/reqbaz-service .`

## What next?
The backend is great on its own, but what makes it useful is a frontend. To get one, take a look at this GitHub project:

**[<i class="icon-link "></i>Requirement Bazaar Web Frontend](https://github.com/rwth-acis/RequirementsBazaar-Dockerfiles/tree/master/reqbaz-web)**

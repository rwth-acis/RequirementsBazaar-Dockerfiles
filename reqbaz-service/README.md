# Requirements Bazaar Backend Service

This Dockerfile retrieves the latest version from the continuous integration server on runtime and serves the backend service on port 8080.

## Run from Docker Hub
The image is built automatically on Docker Hub:

https://registry.hub.docker.com/u/rwthacis/reqbaz-service/

To run it, simply call:

`docker run -d -p 8080:8080 rwthacis/reqbaz-service`

## Build it on your own
Of course you can build the image yourself if you don't want to rely on Docker Hub:

1. `git clone https://github.com/rwth-acis/RequirementsBazaar-Dockerfiles.git`
2. `cd RequirementsBazaar-Dockerfiles/reqbaz-service`
3. `docker build -t rwthacis/reqbaz-service .`

## What next?
The backend is great on its own, but what makes it useful is a frontend. To get one, take a look at this GitHub project:

**[<i class="icon-link "></i>Requirement Bazaar Web Frontend](https://github.com/rwth-acis/RequirementsBazaar-Dockerfiles/tree/master/reqbaz-web)**

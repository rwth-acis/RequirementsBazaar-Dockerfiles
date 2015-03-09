# Requirements Bazaar Web Frontend

This Dockerfile retrieves the latest version from the continuous integration server on runtime and serves the Web frontend on port 80. This is only the Web frontend, you need the backend to get a useful combination. If you haven't started it yet, take a look at this Dockerfile:

**[<i class="icon-link "></i>Requirement Bazaar Service](https://github.com/rwth-acis/RequirementsBazaar-Dockerfiles/tree/master/reqbaz-service)**

## Run from Docker Hub
The image is built automatically on Docker Hub:

https://registry.hub.docker.com/u/rwthacis/reqbaz-web/

To run it, simply call:

`docker run -d -p 80:80 rwthacis/reqbaz-web`

There is an environment variable called `REQBAZ_HOST` where you should enter the address of the backend. If you leave it out, it will fall back to `192.168.59.103` which is the default IP of the boot2docker VM. Just to make sure, type

`boot2docker ip`

of your boot2docker bash. If your backend and frontend run on different hosts, you have to configure the run like this (don't forget the trailing slashes):

`docker run -d -p 80:80 -e "REQBAZ_BACKEND_URI=http://192.168.59.104/" -e "REQBAZ_FRONTEND_URI=http://192.168.59.105/bazaar/" rwthacis/reqbaz-web`

## Build it on your own
Of course you can build the image yourself

1. `git clone https://github.com/rwth-acis/RequirementsBazaar-Dockerfiles.git`
2. `cd RequirementsBazaar-Dockerfiles/reqbaz-web`
3. `docker build -t rwthacis/reqbaz-web .`

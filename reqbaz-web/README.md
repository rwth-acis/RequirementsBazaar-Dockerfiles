# Requirements Bazaar Web Frontend

This Dockerfile retrieves the latest version from the continuous integration server on runtime and serves the Web frontend on port 80. This is only the Web frontend, you need the backend to get a useful combination. If you haven't started it yet, take a look at this Dockerfile:

**[<i class="icon-link "></i>Requirement Bazaar Service](https://github.com/rwth-acis/RequirementsBazaar-Dockerfiles/tree/master/reqbaz-service)**

# Run from Docker Hub
The image is built automatically on Docker Hub:

https://registry.hub.docker.com/u/rwthacis/reqbaz-web/

To run it, simply call:

`docker run -it -p 80:80 rwthacis/reqbaz-web`

# Build it on your own
Of course you can build the image yourself
1. `git clone https://github.com/rwth-acis/RequirementsBazaar-Dockerfiles.git`
2. `cd RequirementsBazaar-Dockerfiles/reqbaz-web`
3. `docker build -t rwthacis/reqbaz-web .`

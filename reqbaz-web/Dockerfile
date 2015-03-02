FROM ubuntu:14.04
MAINTAINER István Koren <koren ÄT dbis.rwth-aachen.de>

# Let the container know that there is no tty
ENV DEBIAN_FRONTEND noninteractive

# Update base image
RUN sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list
RUN apt-get update -y
RUN apt-get upgrade -y

# Install build tools
RUN apt-get install -y \
                     wget \
                     unzip \
                     python

# Create mount point
RUN mkdir /build
WORKDIR /build

# Set default service host
ENV REQBAZ_HOST 192.168.59.103

# Download and unzip newest build from CI server and start the webserver
CMD wget http://layers.dbis.rwth-aachen.de/jenkins/job/Requirements%20Bazaar%20Frontend/lastSuccessfulBuild/artifact/*zip*/archive.zip && \
    unzip archive.zip && \
    cd archive && \
    mv bower_components dist/bower_components && \
    mv app/my-components dist/my-components && \
    cd dist && \
    sed -i 's/localhost:9000/'$REQBAZ_HOST'/g' scripts/scripts*.js && \
    sed -i 's/localhost/'$REQBAZ_HOST'/g' scripts/scripts*.js && \
    sed -i 's/localhost:9000/'$REQBAZ_HOST'/g' views/main.html && \
    python -m SimpleHTTPServer 80

EXPOSE 80

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
                     mysql-server \
                     openjdk-7-jre \
                     dos2unix

# Create mount point
RUN mkdir /build
WORKDIR /build

# Download and unzip newest build from CI server
RUN wget http://layers.dbis.rwth-aachen.de/jenkins/job/Requirements%20Bazaar/lastSuccessfulBuild/artifact/*zip*/archive.zip
RUN unzip archive.zip

# Start the mysql daemon
# dos2unix fixes the "textfile open" error
CMD service mysql start && \
    cd archive && \
    echo "CREATE DATABASE reqbaz;" | mysql -u root && \
    mysql -u root reqbaz < ./etc/ReqBaz_create.sql && \
    mysql -u root reqbaz < ./etc/ReqBaz_demo_data.sql && \
    dos2unix bin/start_network.sh && \
    chmod +x bin/start_network.sh && \
    bin/start_network.sh

EXPOSE 8080

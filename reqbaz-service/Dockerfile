FROM learninglayers/base

MAINTAINER István Koren <koren ÄT dbis.rwth-aachen.de>

# Install dependencies
RUN apt-get install -y \
                     wget \
                     unzip \
                     mysql-client \
                     openjdk-7-jre \
                     dos2unix

# Create mount point
RUN mkdir /build
WORKDIR /build

# Download and unzip newest build from CI server
# dos2unix fixes the "textfile open" error
CMD wget http://layers.dbis.rwth-aachen.de/jenkins/job/Requirements%20Bazaar/lastSuccessfulBuild/artifact/*zip*/archive.zip && \
    unzip archive.zip && \
    cd archive && \
    mysql -u$MYSQL_USER -p$MYSQL_PASSWORD -h$MYSQL_HOST $MYSQL_DATABASE < ./etc/ReqBaz_create.sql && \
    mysql -u$MYSQL_USER -p$MYSQL_PASSWORD -h$MYSQL_HOST $MYSQL_DATABASE < ./etc/ReqBaz_demo_data.sql && \
    sed -i "s/MYSQL_USER/${MYSQL_USER}/g" ./etc/de.rwth.dbis.acis.bazaar.service.BazaarService.properties && \
    sed -i "s/MYSQL_PASSWORD/${MYSQL_PASSWORD}/g" ./etc/de.rwth.dbis.acis.bazaar.service.BazaarService.properties && \
    sed -i "s/MYSQL_HOST/${MYSQL_HOST}/g" ./etc/de.rwth.dbis.acis.bazaar.service.BazaarService.properties && \
    dos2unix bin/start_network.sh && \
    chmod +x bin/start_network.sh && \
    bin/start_network.sh

EXPOSE 8080

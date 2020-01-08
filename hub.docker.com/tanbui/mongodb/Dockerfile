# https://docs.docker.com/engine/examples/mongodb/
# http://cloud-mechanic.blogspot.com/2014/08/docker-simple-service-container-example.html
# Build command
#    docker build -t tanbui/mongodb:3.2 .
# Create the container:
#    docker run --name mongodb -p 27017:27017 tanbui/mongodb:3.2


FROM tanbui/ubuntu_base:14.04

MAINTAINER Tan Bui <trungtanbui@gmail.com>

ENV VOLUME_DATA /data
ENV VOLUME_CONFIG /data/config
ENV VOLUME_LOG /data/log

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927 && \
    echo "deb http://repo.mongodb.org/apt/ubuntu "$(lsb_release -sc)"/mongodb-org/3.2 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-3.2.list && \
    apt-get update && apt-get install -y mongodb-org

RUN mkdir -p $VOLUME_CONFIG && \ 
    mkdir -p $VOLUME_DATA && \
    mkdir -p $VOLUME_LOG  && \
    mkdir -p $VOLUME_LOG/mongodb  && \
    mkdir -p $VOLUME_DATA/mongodb  && \
    touch $VOLUME_DATA/mongodb/mongod.log  && \
    chmod 775 $VOLUME_LOG -R && \
    export LC_ALL=C

ADD mongod.conf /data/config/mongod.conf

EXPOSE 27017

ENTRYPOINT ["/usr/bin/mongod", "--config", "/data/config/mongod.conf"]
CMD ["--quiet"]

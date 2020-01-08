# MongoDB Dockerfile
#
# https://github.com/oscerd/docker-mongodb

# Pull base image.
FROM phusion/baseimage:0.9.16
MAINTAINER Andrea Cosentino <ancosen1985@yahoo.com>

# Install MongoDB
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
RUN echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' > /etc/apt/sources.list.d/mongodb_repo.list
RUN apt-get update 
RUN apt-get install -y mongodb-org
RUN sed 's/^bind_ip/#bind_ip/' -i /etc/mongod.conf

COPY . /src

RUN mkdir -p /data/db
RUN mkdir -p /etc/service/mongodb
RUN cp /src/mongodb-start /etc/service/mongodb/run

# Define mountable directories
VOLUME ["/var/lib/mongodb", "/data/db/"]

EXPOSE 27017 28017

RUN apt-get clean 
RUN rm -rf /var/lib/apt/lists/* 
RUN rm -rf /tmp/* 
RUN rm -rf /var/tmp/*

CMD ["/sbin/my_init"]

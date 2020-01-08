FROM ubuntu:12.04
MAINTAINER Dockerfiles <dockerfiles@docker.com>

# Install MongoDB
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv 7F0CEB10
RUN echo "deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen" | tee -a /etc/apt/sources.list.d/10gen.list
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get -y install mongodb-10gen

# mount a data volume to MongoDB's data directory
VOLUME ["/data/db/"]

# TCP socket
EXPOSE 27017  

# http interface
EXPOSE 28017

# standard command to be run
CMD ["/usr/bin/mongod", "--smallfiles"] 


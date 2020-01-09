##  =====================================================================================  ##
##                            Docker Image for MongoDB Server                              ##
##  =====================================================================================  ##
##         Dockerizing MongoDB: Dockerfile for building MongoDB images                     ##
##         Based on ubuntu:16.04, installs MongoDB following the instructions from:        ##
##         http://docs.mongodb.org/manual/tutorial/install-mongodb-on-ubuntu/              ##
##  =====================================================================================  ##

#  Source Image
FROM ubuntu:16.04

MAINTAINER Baltrushaitis Tomas <tbaltrushaitis@gmail.com>

ENV REFRESHED_AT 2017-01-01

ENV MONGO_MAJOR     3.4
ENV MONGO_VERSION   3.4.0
ENV MONGO_PACKAGE   mongodb-org

RUN UBUNTU_RELEASE="$(cat /etc/lsb-release | grep DISTRIB_CODENAME | cut -d= -f2)"
RUN MONGO_LIST_COMMAND="deb [ arch=amd64,arm64 ] http://repo.mongodb.org/apt/ubuntu ${UBUNTU_RELEASE}/${MONGO_PACKAGE}/${MONGO_MAJOR} multiverse"

#  Import MongoDB public GPG key used by the package management system
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6

#  Create a list file for MongoDB
RUN echo ${MONGO_LIST_COMMAND} | tee /etc/apt/sources.list.d/mongodb-org-${MONGO_MAJOR}.list

#  Add 10gen official apt source to the sources list
#  RUN echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' | tee /etc/apt/sources.list.d/mongodb-10gen.list

#  Update apt-get sources
RUN apt-get -y update                           \
 && apt-get install -y --no-install-recommends  \
 && apt-get -y upgrade

# && apt-get -y install apt-utils   \
# && apt-get clean -y

#  Install the MongoDB packages
RUN apt-get -y install "mongodb"    \
 && apt-get -y clean                \
 && rm -rf /var/lib/apt/lists/*

# /**/

#  Create the MongoDB data directory
RUN mkdir -p "/data/mongodb"   \
 && chown -R mongodb:mongodb "/data/mongodb"

VOLUME ["/storage/docker-assets/mongodb":"/data/mongodb"]

# Set usr/bin/mongod as the dockerized entry-point application
ENTRYPOINT ["/usr/bin/mongod"]

# Expose port 27017 from the container to the host
EXPOSE 27017:28017

# CMD ["mongod"]
CMD [""]

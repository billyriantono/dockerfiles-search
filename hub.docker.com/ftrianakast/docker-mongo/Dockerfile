# use the ubuntu base image provided by dotCloud
FROM ubuntu:13.10
MAINTAINER Felipe Triana, ftrianakast@gmail.com

#install mongo
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
RUN echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' | tee /etc/apt/sources.list.d/10gen.list
RUN dpkg-divert --local --rename --add /sbin/initctl
RUN apt-get update
RUN apt-get install mongodb-10gen
RUN mkdir -p /data/db

# Expose the default port
EXPOSE 27017
  
# Set default container command
ENTRYPOINT /usr/bin/mongod
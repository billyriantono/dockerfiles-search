#
# MongoDB Dockerfile
#
# https://github.com/dockerize/mongodb
#

# Pull base image.

FROM dockerize/ubuntu

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
RUN echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' | sudo tee /etc/apt/sources.list.d/mongodb.list
RUN apt-get update
RUN apt-get install -y mongodb-10gen
RUN mkdir -p /data/db/

EXPOSE 27017 
EXPOSE 28017

CMD ["mongod"]

#
# mongodb server Dockerfile
#
# https://github.com/
#

# Pull base image.
FROM debian:latest

MAINTAINER hihouhou < hihouhou@hihouhou.com >

# Update & install packages for graylog
RUN apt-get update && \
    apt-get install -y mongodb-server

#configure mongo
RUN mkdir -p /data/db/

#Dedicated volume
VOLUME /data/db

EXPOSE 27017

ENTRYPOINT ["/usr/bin/mongod"]

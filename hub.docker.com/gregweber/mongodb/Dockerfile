#
# MongoDB Dockerfile
#
# https://github.com/swyckoff/mongodb
# Locking version.

# Pull base image.
FROM debian
MAINTAINER Greg Weber

ENV MONGO_VERSION 2.4.12
# Install MongoDB.
RUN \
      apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10 && \
      echo 'deb http://downloads-distro.mongodb.org/repo/debian-sysvinit dist 10gen' > /etc/apt/sources.list.d/mongodb.list && \
      apt-get update && \
      apt-get install -y adduser mongodb-10gen=$MONGO_VERSION
      rm -rf /var/lib/apt/lists/*

# Define mountable directories.
VOLUME ["/data/db"]

# Define working directory.
WORKDIR /data

# Define default command.
CMD ["mongod"]

# Expose ports.
#   - 27017: process
#   - 28017: http
EXPOSE 27017
EXPOSE 28017

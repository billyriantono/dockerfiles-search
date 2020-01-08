FROM debian:latest

# Add 10gen official apt source to the sources list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv 7F0CEB10
RUN echo 'deb http://downloads-distro.mongodb.org/repo/debian-sysvinit dist 10gen' | tee /etc/apt/sources.list.d/mongodb.list

# Install MongoDB
RUN apt-get update 
RUN apt-get install adduser
#RUN apt-get install mongodb-10gen
RUN apt-get install -y mongodb-org=2.6.1

# Create the MongoDB data directory
RUN mkdir -p /data/db
RUN mkdir -p /data/configdb


# Define montable directories
WORKDIR /data

#ENTRYPOINT ["mongod"]

EXPOSE 27017
EXPOSE 27019
EXPOSE 28017

# Dockerizing MongoDB: Dockerfile for building MongoDB images
# Based on ubuntu:16.04, installs MongoDB following the instructions from:
# http://docs.mongodb.org/manual/tutorial/install-mongodb-on-ubuntu/

FROM       ubuntu:latest

# Installation:
# Import MongoDB public GPG key AND create a MongoDB list file
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6 
RUN echo "deb [ arch=amd64,arm64 ] http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.4 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-3.4.list

# Update apt-get sources AND install MongoDB
RUN apt-get update && apt-get install -y mongodb-org

#Install mongo client
#RUN apt-get -y install mongo-client

#Install nano  text editor
RUN apt-get -y install nano

# Create the MongoDB data directory
RUN mkdir -p /var/data/mongodb

#Create a volume
#VOLUME ["/var/data/mongodb"]

# Expose port #27017 from the container to the host
EXPOSE 27017

#Create a aux directory for scripts
RUN mkdir -p /usr/scripts

#Copy config
COPY mongod.conf /etc/

#Copy script
COPY initMongo.sh /usr/scripts/
COPY createUser.js /usr/scripts/

#Add exec permission
RUN chmod +x /usr/scripts/initMongo.sh
RUN chmod +x /usr/scripts/createUser.js


#Starts Mongo and creates admin user
RUN /usr/scripts/initMongo.sh

#Create a volume
VOLUME ["/var/data/mongodb"]

# Set /usr/bin/mongod as the dockerized entry-point application
ENTRYPOINT ["/usr/bin/mongod","--auth", "--dbpath", "/var/data/mongodb"]
#ENTRYPOINT ["/usr/bin/mongod", "--dbpath", "/var/data/mongodb", "--logpath","/var/log/mongodb/mongodb.log"]

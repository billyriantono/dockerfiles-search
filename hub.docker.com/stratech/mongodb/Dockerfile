#++++++++++++++++++++++++++++++++++++++
# stratech/mongodb
#++++++++++++++++++++++++++++++++++++++
# mongodb 
#++++++++++++++++++++++++++++++++++++++

FROM stratech/ubuntu:14.04
MAINTAINER Stefano Mazzega <stefano.mazzega@gmail.com>

CMD ["/sbin/my_init"]

# Some Environment Variables
ENV    DEBIAN_FRONTEND noninteractive

# Ensure UTF-8
ENV LANG       en_US.UTF-8
ENV LC_ALL     en_US.UTF-8

RUN locale-gen en_US.UTF-8

RUN apt-get -y --force-yes update

# Installation:
# Import MongoDB public GPG key AND create a MongoDB list file
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
RUN echo "deb http://repo.mongodb.org/apt/ubuntu "$(lsb_release -sc)"/mongodb-org/3.0 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-3.0.list

# Update apt-get sources AND install MongoDB
RUN apt-get -y --force-yes update && apt-get install -y mongodb-org

# Create the MongoDB data directory
RUN mkdir -p /data/db

RUN mkdir -p /etc/service/mongod
ADD start.sh /etc/service/mongod/run
RUN chmod +x /etc/service/mongod/run

EXPOSE 27017

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# base image
FROM    centos:centos6

# author
MAINTAINER Serj Kazar

# Enable EPEL for Node.js
RUN     rpm -Uvh http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm

# Install Node.js and npm
RUN     yum install -y npm

# Bundle app source
ADD . /src

# Install app dependencies
RUN cd /src; npm install

# expose ports
EXPOSE 80

CMD ["node", "/src/src/bin/www"]

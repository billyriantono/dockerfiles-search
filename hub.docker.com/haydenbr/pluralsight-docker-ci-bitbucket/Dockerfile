FROM centos:centos6

MAINTAINER nigelpoulton@hotmail.com

# Enable EPEL for Node.js
RUN rpm -Uvh http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm

# Install Node...
RUN yum install -y npm
ADD package.json /src/package.json
RUN cd /src && npm install

EXPOSE 8080

# Copy app to /src
WORKDIR /src
ADD . /src

ENTRYPOINT [ "node", "./app.js" ]
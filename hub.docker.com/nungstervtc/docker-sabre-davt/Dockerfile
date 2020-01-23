FROM centos:centos6

LABEL MAINTAINER nigelpoulton@hotmail.com

# Enable EPEL for Node.js
RUN rpm -Uvh http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm

# Install Node...
RUN yum install -y npm

# Copy app to /src
COPY . /src

# Install app and dependencies into /src
RUN cd /src && \
    npm config set registry http://registry.npmjs.org/ && \
    npm install

EXPOSE 8080

CMD cd /src && node ./app.js
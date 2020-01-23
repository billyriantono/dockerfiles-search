#RUN, FROM, MAINTAINER, ADD, CMD, ENTRYPOINT, ENV, EXPOSE,
#USER, VOLUME, WORKDIR
#RPM - without dependencies 
FROM centos:centos6

MAINTAINER nigelpoulton@hotmail.com

# Enable EPEL for Node.js
#RUN rpm -Uvh http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm

RUN yum install -y epel-release

# Install Node...
CMD echo "Start nodejs installation"
RUN yum install -y sudo
RUN yum install -y gcc-c++ make
RUN curl -sL https://rpm.nodesource.com/setup_6.x | sudo -E bash -
RUN yum install -y nodejs
RUN node -v 
#RUN yum install -y npm
RUN npm -v
# Copy app to /src
COPY . /src

# Install app and dependencies into /src
#RUN cd /src; npm install
RUN cd /src; npm install -g npm@latest
EXPOSE 8080

CMD cd /src && node ./app.js
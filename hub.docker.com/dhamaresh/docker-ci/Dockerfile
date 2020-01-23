FROM centos:centos6

MAINTAINER dhamaresh@gmail.com

# Enable EPEL for Node.js
RUN rpm -Uvh http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm

# Install Node
RUN yum install -y npm

# Copy app to /src folder
COPY . /src

# Install app and dependencies into /src folder
RUN cd /src; npm install

#expose 8080 port

EXPOSE 8080

#Run your app

CMD cd /src && node ./app.js

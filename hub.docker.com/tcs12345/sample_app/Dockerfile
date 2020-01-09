FROM centos:latest

MAINTAINER tcs

# Enable EPEL for Node.js
#RUN rpm -Uvh http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm
RUN curl -sL https://rpm.nodesource.com/setup | bash -
RUN  yum -y update
RUN yum install -y nodejs
RUN yum install -y nodejs --nogpgcheck
# Install Node...
#RUN  yum install -y npm 

# Copy app to /src
COPY . /src

# Install app and dependencies into /src
RUN cd /src; npm install

EXPOSE 8080

CMD cd /src && node ./app.js

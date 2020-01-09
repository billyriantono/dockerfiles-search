FROM circleci/node:latest

MAINTAINER nandito3555@hotmail.com

# Enable EPEL for Node.js
# RUN rpm -Uvh http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm

# # Install Node...
# RUN yum install -y npm

RUN sudo mkdir /app  
# Copy app to /app
COPY . /app

# Install app and dependencies into /app
RUN cd /app; sudo npm install

EXPOSE 8080

CMD cd /app && node ./app.js
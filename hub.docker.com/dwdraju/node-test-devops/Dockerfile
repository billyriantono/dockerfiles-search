FROM ubuntu:14.04

MAINTAINER Raju Dawadi rajudawadinp@gmail.com

ENV DEBIAN_FRONTEND noninteractive

# Install Nodejs
RUN apt-get update && apt-get install -y nodejs npm nodejs-legacy

# Copy app to /src
COPY . /src

# Install app and dependencies into /src
RUN cd /src; 

#Show in our container
EXPOSE 8081

#Run the app
CMD cd /src && nodejs ./index.js

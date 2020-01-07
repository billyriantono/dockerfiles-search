FROM centos:centos6

MAINTAINER nigelpoulton@hotmail.com

# Enabling EPEL for Node.js
RUN rpm -Uvh http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm

# Install Node...
RUN yum install -y nginx

# Copy app to /src
COPY . /src

# Install app and dependencies into /src

EXPOSE 8080


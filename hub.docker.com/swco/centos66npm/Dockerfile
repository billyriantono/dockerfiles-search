FROM centos:centos6.6
MAINTAINER Liam Galvin

WORKDIR /srv

RUN yum -y update && yum clean all

RUN yum install -y -q epel-release && yum clean all

RUN yum install -y fontconfig freetype libfreetype.so.6 libfontconfig.so.1 bzip2 tar && yum clean all

# NPM
RUN yum install -y npm && yum clean all

# Update NPM
RUN npm install -g npm

# Grunt (globally)
RUN npm install -g grunt-cli

RUN npm config set cache /tmp/.npm
RUN npm config set userconfig /tmp/.npmrc
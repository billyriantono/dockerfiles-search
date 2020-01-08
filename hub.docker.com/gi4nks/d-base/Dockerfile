#FROM debian:jessie
FROM node:5.3-slim
MAINTAINER gi4nks "gnlc.lupo@gmail.com"

# --------------------------
# Debian:jessie
# -------------
# - Subversion: 1.8
# - Git: distribution default
# - unzip: distribution default
# - wget: distribution default
# - rake: distribution default
# - telnet: distribution default
# - vim: distribution default
# - curl: distribution default
# - supervisor: distribution default
# --------------------------

# this is a non-interactive automated build - avoid some warning messages
ENV DEBIAN_FRONTEND noninteractive

# install additional libraries
RUN apt-get update --fix-missing -yq && \
apt-get install -yq git net-tools vim && \
rm -rf /var/lib/apt/lists/* && \
apt-get clean

# Note the new setup script name for Node.js v0.12
#RUN curl -sL https://deb.nodesource.com/setup_4.x | bash -

# Then install with:
#RUN apt-get install -y nodejs && \
#  rm -rf /var/lib/apt/lists/* && \
#  apt-get clean
  
# Installing needed npm packages
RUN npm install karma-cli -g && \
    npm install grunt-cli -g && \
    npm install bower -g && \
    npm install yo -g && \
    npm install browserify -g && \
    npm install browser-sync -g 

# Add a yeoman user because grunt doesn't like being root
RUN adduser --disabled-password --gecos "" yeoman && \
  echo "yeoman ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

RUN mkdir /data && chown yeoman:yeoman /data

# Define working directory.
WORKDIR /data
# Always run as the yeoman user
USER yeoman
CMD /bin/bash



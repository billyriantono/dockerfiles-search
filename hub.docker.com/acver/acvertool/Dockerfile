FROM centos:centos6


MAINTAINER Jerome.Helbling@ac-versailles.fr
MAINTAINER david.messager@ac-versailles.fr
MAINTAINER michael.nourry@ac-versailles.fr


# Enable Extra Packages for Entreprise Linux (EPEL) for CentOS
RUN yum install -y epel-release

# Install Git
RUN yum install -y git

# use git over https
# RUN git config --system url."https://".insteadOf git://

# Install Node.js and npm
RUN yum install -y nodejs npm

# Install app dependencies

RUN npm config set registry "http://registry.npmjs.org/" 
RUN npm install -g inherits 
RUN npm install -g bower 
RUN bower update --allow-root 
RUN npm install -g grunt-cli 

# Exec
WORKDIR /src/ressources/build
CMD grunt prod && grunt watch


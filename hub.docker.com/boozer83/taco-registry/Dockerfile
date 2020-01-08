FROM centos:7
MAINTAINER startlkj <starlkj@exntu.com>

RUN yum update -y
RUN yum install -y epel-release 
RUN yum install -y git nodejs npm
RUN npm install @angular/cli

RUN mkdir /app
WORKDIR /app

RUN git clone https://exntu.metatron:'dlrudwls78!'@tde.sktelecom.com/stash/scm/oreotools/c-registry.git

WORKDIR /app/c-registry/registry

RUN npm install

EXPOSE 4200
CMD [ "npm", "start" ]


FROM ubuntu

MAINTAINER Martin GOYOT <martin.goyot@enalean.com>

RUN apt-get update
RUN apt-get install -y nodejs
RUN apt-get install -y npm

RUN ln -s /usr/bin/nodejs /usr/bin/node
RUN npm install -g node-inspector
RUN npm install -g nodemon
RUN npm install -g nodev
RUN npm install -g node-monkey

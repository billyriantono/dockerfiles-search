FROM node:5.0.0
MAINTAINER Souranil Sen <souranil@gmail.com>

RUN mkdir /src
ENV NODE_ENV='production'
RUN apt-get -y -qq install python

# Expose the app server port
EXPOSE 8080

RUN apt-get update \
	&& apt-get install -y wget make g++ \
	&& apt-get install -y build-essential

## TODO: In production copy files and run from there !!
RUN npm install -g node-gyp
ADD package.json /src/package.json
RUN cd /src && npm install

ADD . /src
# Set working directory
WORKDIR	/src



ENTRYPOINT ["bash", "-c", "node server.js"]


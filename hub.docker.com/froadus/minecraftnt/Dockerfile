FROM node:latest

# File Author / Maintainer
MAINTAINER frederic grati

RUN mkdir /src

# Install nodemon
RUN npm install -g nodemon

# Define working directory
WORKDIR /src
ADD . /src

# Provides cached layer for node_modules
ADD package.json /tmp/package.json
RUN cd /tmp && npm install
RUN mkdir -p /src && cp -a /tmp/node_modules /src/

# Expose port
EXPOSE  3000

# Start app
CMD npm start
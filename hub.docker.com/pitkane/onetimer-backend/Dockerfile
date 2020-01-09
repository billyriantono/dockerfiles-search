FROM node:latest

RUN apt-get update
RUN apt-get install -y vim

# create app directory in container
RUN mkdir -p /app

# http://bitjudo.com/blog/2014/03/13/building-efficient-dockerfiles-node-dot-js/
ADD package.json /tmp/package.json
ADD package-lock.json /tmp/package-lock.json
RUN cd /tmp && npm install --silent
RUN mkdir -p /app && mv /tmp/node_modules /app/

# From here we load our application's code in, therefore the previous docker
# "layer" thats been cached will be used if possible
WORKDIR /app
# ADD . /app

EXPOSE 5200

CMD ["npm", "start"]

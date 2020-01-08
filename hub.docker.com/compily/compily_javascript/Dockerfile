FROM ubuntu:16.04
MAINTAINER Ephraim Rothschild
RUN mkdir -p /compilebox/usercode && chmod -R 777 /compilebox/usercode

# Update the repository sources list
RUN apt-get update

# For NodeJS
RUN apt-get install -y nodejs
RUN apt-get install -y npm
RUN npm install -g underscore request express jade shelljs passport http sys jquery lodash async mocha moment connect validator restify ejs ws co when helmet wrench brain mustache should backbone forever  debug && export NODE_PATH=/usr/local/lib/node_modules/
RUN apt-get install -y clojure1.6

RUN apt-get install -y bc



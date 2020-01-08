FROM ubuntu:16.04

LABEL maintainer="Node Docker Maintainers in RUBY <developement@ozex.io>"

RUN apt-get update
RUN apt-get install sudo

# Install Node.js
RUN apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -

RUN apt-get install -y nodejs
RUN apt-get install -y build-essential

# Bundle app source
# Trouble with COPY http://stackoverflow.com/a/30405787/2926832
COPY ./src /src

# Install app dependencies
RUN cd /src; npm install

# Binds to port 8080
EXPOSE  5090

#  Defines your runtime(define default command)
# These commands unlike RUN (they are carried out in the construction of the container) are run when the container
CMD ["node", "/src/server.js"]
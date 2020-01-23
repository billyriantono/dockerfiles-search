FROM ubuntu:latest  
MAINTAINER alhexanderad@gmail.com

#Update
RUN apt-get update \
    && apt-get -qq update \
    && apt-get install -y nodejs npm

RUN update-alternatives --install /usr/bin/node node /usr/bin/nodejs 10

RUN apt-key adv --keyserver pgp.mit.edu --recv D101F7899D41F3C3 \
    && echo "deb http://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
    && apt-get update \
    && apt-get install yarn


# Create app directory
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

# Install app dependencies
COPY package.json /usr/src/app/
RUN yarn add express --dev

# Bundle app source
COPY server.js /usr/src/app

EXPOSE 9090
CMD yarn run start
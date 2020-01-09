# Use an official Node runtime as a parent image
FROM node:11.6

# set working directory
RUN mkdir -p /usr/src/app

WORKDIR /usr/src/app

# Add `/usr/src/app/node_modules/.bin` to $PATH and set port
ENV PATH /usr/src/app/node_modules/.bin:$PATH

# install and cache app dependencies
COPY package.json /usr/src/app/package.json

RUN npm install
RUN npm i -g @angular/cli

# Set the working directory to /usr/src/app
COPY . /usr/src/app

# start app
CMD ng serve --host 0.0.0.0 --port 2000

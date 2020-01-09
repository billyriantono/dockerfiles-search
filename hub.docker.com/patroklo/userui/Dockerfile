# base image
FROM node:10.15.3-stretch

ARG env
ENV environment $env
# set working directory
RUN mkdir /usr/src/app
WORKDIR /usr/src/app

# add `/usr/src/app/node_modules/.bin` to $PATH
ENV PATH /usr/src/app/node_modules/.bin:$PATH

# install and cache app dependencies
COPY package.json /usr/src/app/package.json
RUN npm install
RUN npm install -g @angular/cli@latest

# add app
COPY . /usr/src/app

# build app
#CMD ng build -c dev

# start app
CMD ng serve --host 0.0.0.0 -c $environment

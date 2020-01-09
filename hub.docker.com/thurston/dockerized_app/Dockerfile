FROM node:4-onbuild

MAINTAINER Alex Conceiro (conceiro@gmail.com)

# run node in a production environment
ENV NODE_ENV=production

# Add our user and group first to make sure their IDs get assigned consistently
RUN groupadd -r app && useradd -r -g app app

# Create app directory
RUN mkdir -p /usr/src/dockerized_app
WORKDIR /usr/src/dockerized_app

# Install app dependencies
COPY package.json /usr/src/dockerized_app/
RUN npm install

# Bundle app source
COPY . /usr/src/dockerized_app

# replace this with your application's default port
EXPOSE 80

# run npm start script
CMD [ "npm", "start" ]

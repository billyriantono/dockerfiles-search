FROM node:boron

# Create app directory
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

# Install app dependencies
COPY package.json /usr/src/app/
RUN npm install

# Grab configs
COPY webpack.config.js /usr/src/app/
COPY .babelrc /usr/src/app/

# Bundle app source
RUN mkdir -p /usr/src/app/src
RUN mkdir -p /usr/src/app/lib

COPY ./src/ /usr/src/app/src
COPY ./lib/ /usr/src/app/lib

CMD [ "npm", "start" ]
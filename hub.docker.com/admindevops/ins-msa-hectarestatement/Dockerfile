# Set NodeJS version
FROM node:8

# Create app directory
WORKDIR /usr/src/app

# Install app dependencies
COPY package.json /usr/src/app

# Install required packages
RUN npm install

# GeoJSON Reducer
RUN npm install -g geojson-reducer

# Bundle app source
COPY . /usr/src/app

# Setup port
EXPOSE 3009

# Running command
CMD [ "node", "server.js" ]

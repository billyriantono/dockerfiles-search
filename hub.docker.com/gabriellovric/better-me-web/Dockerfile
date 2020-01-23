FROM node:alpine

# Create app directory
WORKDIR /opt/app

# Install app dependencies
COPY package*.json /opt/app/

RUN npm install
RUN npm install webpack -g
RUN npm install webpack-cli -g

# Bundle app source
COPY src/ /opt/app/src/
COPY .babelrc /opt/app/
COPY webpack.config.js /opt/app/

RUN webpack

# Run node server
COPY server.js /opt/app/

EXPOSE 8080
CMD [ "npm", "start" ]
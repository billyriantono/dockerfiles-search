FROM node:10

# Create app directory
RUN mkdir -p /usr/src/FCMNotificationManagement
WORKDIR /usr/src/FCMNotificationManagement           

# Bundle app source
COPY . /usr/src/FCMNotificationManagement

# Install app dependencies
RUN WITH_SASL=0 npm install

CMD [ "node", "server.js"]



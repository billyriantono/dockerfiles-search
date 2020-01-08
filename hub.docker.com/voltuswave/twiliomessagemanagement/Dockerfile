FROM node:10

# Create app directory
RUN mkdir -p /usr/src/TwilioMessageManagement
WORKDIR /usr/src/TwilioMessageManagement           

# Bundle app source
COPY . /usr/src/TwilioMessageManagement

# Install app dependencies
RUN WITH_SASL=0 npm install

CMD [ "node", "server.js"]



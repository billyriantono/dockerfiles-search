FROM node:10

# Create app directory
RUN mkdir -p /usr/src/SmsEntityManagement
WORKDIR /usr/src/SmsEntityManagement           

# Bundle app source
COPY . /usr/src/SmsEntityManagement

# Install app dependencies
RUN WITH_SASL=0 npm install

RUN npm install newrelic

COPY newrelic.js /usr/src/SmsEntityManagement/node_modules/newrelic/

CMD [ "node", "server.js"]



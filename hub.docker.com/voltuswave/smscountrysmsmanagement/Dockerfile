FROM node:10

# Create app directory
RUN mkdir -p /usr/src/SmsCountrySmsManagement
WORKDIR /usr/src/SmsCountrySmsManagement           

# Bundle app source
COPY . /usr/src/SmsCountrySmsManagement

# Install app dependencies
RUN WITH_SASL=0 npm install

CMD [ "node", "server.js"]



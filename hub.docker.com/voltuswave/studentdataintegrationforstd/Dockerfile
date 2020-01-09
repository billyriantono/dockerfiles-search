FROM node:8

# Create app directory
RUN mkdir -p /usr/src/StudentsDataIntegration
WORKDIR /usr/src/StudentsDataIntegration           

# Bundle app source
COPY . /usr/src/StudentsDataIntegration

# Install app dependencies
RUN WITH_SASL=0 npm install

CMD [ "node", "server.js"]



FROM node:10

# Create app directory
RUN mkdir -p /usr/src/TemplateEntityManagement
WORKDIR /usr/src/TemplateEntityManagement          

# Bundle app source
COPY . /usr/src/TemplateEntityManagement

# Install app dependencies
RUN WITH_SASL=0 npm install

CMD [ "node", "server.js"]



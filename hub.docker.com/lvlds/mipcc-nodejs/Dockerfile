FROM node:5.12-slim

# Create app directory
RUN mkdir -p /usr/src/app/log /usr/src/app/service-account 
WORKDIR /usr/src/app

# Install app dependencies
COPY package.json /usr/src/app/
RUN npm install forever -g && npm install

# Bundle app source
COPY . /usr/src/app

VOLUME ["/service-account"]

EXPOSE 8080
CMD ["node", "index.js"]
FROM node:carbon-slim

# Create app directory
WORKDIR /git/bookswapp-api

# Install app dependencies
COPY package.json /git/bookswapp-api/
RUN npm install

# Bundle app source
COPY . /git/bookswapp-api/
RUN npm run prepublish

CMD [ "npm", "run", "runServer" ]
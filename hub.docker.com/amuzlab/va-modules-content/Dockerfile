FROM node:carbon-slim

# Create app directory
WORKDIR /git/sa_api_gateway_ms

# Install app dependencies
COPY package.json /git/sa_api_gateway_ms/
RUN npm install
# npm install --save graphql-type-json
# Bundle app source
COPY . /git/sa_api_gateway_ms/
RUN npm run prepublish

CMD [ "npm", "run", "runServer" ]

EXPOSE 5000

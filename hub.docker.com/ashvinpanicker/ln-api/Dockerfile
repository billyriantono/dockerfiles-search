# Use slim version of node to reduce container size (change to node:8 or 9 if it doesn't work)
FROM node:slim

# Create app directory
WORKDIR /usr/src/ln-api

# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
COPY package*.json ./

RUN npm install
# If you are building your code for production
# RUN npm ci --only=production
# TODO Learn Circle CI :P

# Bundle app source
COPY . .
# ^This should copy everything in current dir to docker container workdir

# ln-api server runs on port 3000 so we are exposing it so that it is accessible outside container
EXPOSE 3000

# Set proxy server to run on port 80
ENV http_proxy 80:3000
ENV https_proxy 80:3000

# Run `npm start` , Note that `npm install` happened earlier
CMD [ "npm", "start" ]
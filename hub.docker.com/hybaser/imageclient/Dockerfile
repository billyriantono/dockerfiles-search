# base image
FROM node:12.2.0-alpine

# set working directory
WORKDIR /app/imageclient

# install and cache app dependencies
COPY package.json ./
RUN npm install --silent
COPY . .

# start app
CMD ["npm", "start"]
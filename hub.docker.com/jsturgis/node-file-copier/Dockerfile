FROM node:alpine

RUN adduser -S jeff
RUN apk update && apk add rsync openssh-client

# Create app directory
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

# Install app dependencies
COPY package.json /usr/src/app/
RUN yarn install --production

# Bundle app source
COPY . /usr/src/app

USER jeff
CMD [ "yarn", "start" ]

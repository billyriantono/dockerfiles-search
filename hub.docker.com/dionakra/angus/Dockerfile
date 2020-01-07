FROM mhart/alpine-node:0.12.18

# Add git
RUN apk update && apk upgrade && \
apk add --no-cache bash git openssh

# Add all necessary packes to build node-gyp
RUN apk add --no-cache --virtual .build-deps make gcc g++ python 

# Install Angus & Bower globally
RUN npm install -g traycold/angus --production --silent \
 && npm install -g bower --production --silent

# Once everything is installed, remove unnecesary dependencies
RUN apk del .build-deps

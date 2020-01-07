FROM node:8.11.2

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y build-essential curl git && \
npm install -g nodemon gulp pm2 mocha

RUN DEBIAN_FRONTEND=noninteractive mkdir /var/app
WORKDIR /var/app

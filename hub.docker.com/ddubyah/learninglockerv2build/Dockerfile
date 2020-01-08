# BASED ON NODE:9.1
FROM node:9.1 as base

# Dependencies
RUN  apt-get update \
  && apt-get install -y \
  apt-transport-https \
  build-essential \
  curl \
  git \
  python \
  xvfb

# required global node modules
RUN npm install -g yarn pm2

# set up pm2 service monitor
RUN pm2 install pm2-logrotate && \
  pm2 set pm2-logrotate:compress true

USER root

# get the LearninLocker code
RUN git clone https://github.com/LearningLocker/learninglocker.git

# Enter directory and install requirements
WORKDIR learninglocker
RUN yarn install

# copy env files
COPY config/webapp.env /learninglocker/.env

# Build ALL services N.B. May be more parsimonious to only build the service we want to run per container. We'll build all for now
RUN yarn build-all

# Grab the xAPI service source
WORKDIR /
RUN git clone https://github.com/LearningLocker/xapi-service.git

COPY config/xapi.env /xapi-service/.env
WORKDIR xapi-service
RUN npm install
RUN npm run build

EXPOSE 3000 8080 8081

CMD ["/bin/bash"]

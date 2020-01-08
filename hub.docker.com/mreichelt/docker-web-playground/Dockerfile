# use latest Node LTS (Carbon)
FROM node:carbon

# set user to avoid permission issues
# (see https://github.com/nodejs/node-gyp/issues/1236)
USER node
RUN mkdir /home/node/.npm-global
ENV PATH=/home/node/.npm-global/bin:$PATH
ENV NPM_CONFIG_PREFIX=/home/node/.npm-global

# install tools we need
RUN npm install -g firebase-tools@4.2.0 grunt-cli@1.3.2 sass@1.14.3 ruby@0.6.1

# reset user back to root
USER root

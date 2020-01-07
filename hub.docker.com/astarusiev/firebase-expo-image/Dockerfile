# use Node 10.15
FROM node:10.15

# set user to avoid permission issues
# (see https://github.com/nodejs/node-gyp/issues/1236)
USER node
RUN mkdir /home/node/.npm-global
ENV PATH=/home/node/.npm-global/bin:$PATH
ENV NPM_CONFIG_PREFIX=/home/node/.npm-global

# install Firebase CLI
RUN npm install -g firebase-tools
# install Expo CLI globally
RUN npm install -g expo-cli
# install Yarn globally
RUN npm install -g yarn

# reset user back to root
USER root
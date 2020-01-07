FROM node:latest
MAINTAINER Pablo Rodriguez V. <prodriguez.val@gmail.com>

#####################################
# Install Angular CLI
# Install Yarn
#####################################
RUN npm install -g @angular/cli && \
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    apt-get update && apt-get install apt-transport-https && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && apt-get install yarn

#####################################
# Non-Root User: node
#####################################
USER node
ARG NODE_ENV=dev
ENV NODE_ENV=${NODE_ENV}

#####################################
# ng serve port
#####################################
EXPOSE 4200

#####################################
# Live reload port
#####################################
EXPOSE 49153

#####################################
# Set yarn as default package manager
#####################################
RUN ng set --global packageManager=yarn

ENV WORKSPACE=/home/node/
WORKDIR $WORKSPACE
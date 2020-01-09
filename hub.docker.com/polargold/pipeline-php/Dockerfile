FROM php:7.3-cli

LABEL maintainer="michaels@polargold.de"

USER root

RUN apt update && apt install -y gnupg curl unzip git rsync
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt update && apt install -y yarn
RUN yarn global add npm
RUN npm install -g n

# docker build -t polargold/jenkins-slave-php:<7.0, 7.1, 7.2> .
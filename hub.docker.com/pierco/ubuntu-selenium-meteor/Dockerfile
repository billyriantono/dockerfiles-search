FROM ubuntu:latest

RUN apt-get update
RUN apt-get install -y locales
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    dpkg-reconfigure --frontend=noninteractive locales && \
    update-locale LANG=en_US.UTF-8

RUN apt-get install -y \
    default-jre \
    build-essential \
    xvfb \
    curl \
    node-gyp \
    firefox \
    npm

RUN npm i -g n
RUN n latest

RUN npm install -g chimp --unsafe-perm
RUN curl https://install.meteor.com/ | sh


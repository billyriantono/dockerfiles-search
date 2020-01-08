FROM node:lts-jessie

MAINTAINER Yu Shi <tttptd@yandex.com>

# RUN npm install npm -g
RUN npm i -g npm@6

# Add a symbolic link for Node
RUN ln -s /usr/bin/nodejs /usr/bin/node

# Source the bash
RUN . ~/.bashrc

# Clean up
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

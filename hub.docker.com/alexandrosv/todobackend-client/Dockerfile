FROM ubuntu:trusty
MAINTAINER Alejandro Villamarin <favm@email.com>

# Suppress dpkg errors
ENV TERM=xterm-256color

# Set mirrors to CZ
#RUN sed -i "s/https:\/\/archive./https:\/\/cz.archive./g" /etc/apt/sources.list

# Install node.js
RUN apt-get update && \
    apt-get install curl git -y && \
    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash - && \
    apt-get install -y nodejs 

ADD . /app
WORKDIR /app

# Install application dependencies
RUN npm install -g grunt-cli && \
    npm install --unsafe-perm=true

# Set entrypoint
CMD ["node","app.js"]
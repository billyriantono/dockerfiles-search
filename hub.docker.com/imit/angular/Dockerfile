
FROM debian:jessie

MAINTAINER luiz@quelves.com

EXPOSE 3000 4200

ENV NODE_ENV development

# Install Utilities
RUN apt-get update -q  \
 && apt-get install -yqq \
 curl \
 git \
 ssh \
 gcc \
 make \
 build-essential \
 libkrb5-dev \
 sudo \
 gnupg \
 apt-utils \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Set root passwd 
# Add admin user so that container does not run as root 
RUN echo "root:Dev.2017" | chpasswd && \
 chmod u+w /etc/sudoers && \
 echo "admin  ALL=(ALL)       ALL" >> /etc/sudoers && \
 chmod u-w /etc/sudoers && \
 useradd -m admin && \
 echo "admin:Dev.2017" | chpasswd  && \
 usermod -s /bin/bash admin 

 RUN sudo curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash - && \
    sudo apt-get install -y nodejs && \
    sudo npm install npm@latest -g  && \
    sudo npm -g config set user root && \
    sudo npm install -g node-gyp && \
    sudo npm install -g @angular/cli 


USER admin

WORKDIR /app

CMD npm install && npm start





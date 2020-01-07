
FROM node:latest

RUN apt-get update 
RUN apt-get install -y git 

RUN curl https://install.meteor.com/ | sh 
RUN apt-get install -y openssh-client 
RUN echo 'PATH="/usr/local/node/bin:${PATH}"' >> /etc/bash.bashrc 

RUN  npm install --global mup
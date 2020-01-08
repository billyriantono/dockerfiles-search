FROM node:latest
MAINTAINER Paul Oosthuysen (paul.oosthuysen@britehouse.co.za)

RUN which ssh-agent || ( apt-get update -y && apt-get install openssh-client -y ) && npm install grunt-cli bower -g
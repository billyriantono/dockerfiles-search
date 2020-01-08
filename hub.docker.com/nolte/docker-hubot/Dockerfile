# Dockerfile
FROM ubuntu:latest

RUN apt-get update
RUN apt-get install nodejs-legacy npm --yes
RUN npm install -g npm


RUN npm install -g yo generator-hubot

RUN useradd -ms /bin/bash hubot

USER hubot
WORKDIR /home/hubot

RUN yo hubot --owner="You" --name="HuBot" --description="HuBot on Docker" --defaults

RUN npm install hubot-irc --save && npm install


# remove heroku live check not needed for the docker file
RUN npm uninstall hubot-heroku-keepalive --save && npm install
RUN sed '/hubot-heroku-keepalive/d' ./external-scripts.json > /tmp/external-scripts.json
RUN mv /tmp/external-scripts.json /home/hubot/external-scripts.json
RUN chmod u+x ./external-scripts.json


CMD bin/hubot -a irc --name myhubot
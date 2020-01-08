FROM node:6.3.0-slim
MAINTAINER rprev

ENV HL_HOME /home/hubot

RUN npm install -g yo generator-hubot hubot coffee-script \
 && useradd hubot \
 && mkdir ${HL_HOME} \
 && chown hubot:hubot ${HL_HOME}

USER hubot

WORKDIR ${HL_HOME}

RUN yo hubot --owner "noname" --name "hubot-letschat" --description "Hubot for Let's Chat" --adapter lets-chat

CMD bin/hubot -a lets-chat

FROM alpine:latest
MAINTAINER Marcos Sánchez <arkanus@gmail.com>

RUN apk add --no-cache nodejs &&\
    npm install -g npm &&\
    npm install -g yo generator-hubot coffee-script &&\
    mkdir /hubot &&\
	adduser -D hubot &&\
	chown -R hubot:hubot /hubot

USER hubot
WORKDIR /hubot
RUN yo hubot --name=shalldoek --description="Dog-Sucking bot" --defaults &&\
    npm install hubot-slack --save

ENV HUBOT_NAME=hubot\
    HUBOT_ADAPTER=slack


CMD ["/hubot/bin/hubot", "--adapter $HUBOT_ADAPTER", "--name $HUBOT_NAME"]

FROM node:latest
MAINTAINER Masato Yamazaki <mas9612@gmail.com>

# install hubot generator
RUN npm install -g yo generator-hubot

# add new user to avoid permission problem when generate bot
RUN adduser --disabled-password hubot --gecos "" && \
        echo "hubot ALL=(ALL) NOPASSWORD:ALL" >> /etc/sudoers
ENV HOME /home/hubot
USER hubot

# generate hubot
RUN mkdir $HOME/bot
WORKDIR $HOME/bot
RUN yo hubot --defaults --adapter=slack

CMD HUBOT_SLACK_TOKEN=$SLACK_TOKEN bin/hubot --adapter slack

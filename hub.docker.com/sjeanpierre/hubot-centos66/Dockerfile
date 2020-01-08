FROM tcnksm/centos-node:0.11

RUN npm install -g coffee-script hubot

RUN mkdir -p /var/hubot/
WORKDIR /var/hubot/
COPY . /var/hubot/

ONBUILD COPY package.json /var/hubot/
ONBUILD RUN npm install
ONBUILD COPY . /var/hubot/scripts

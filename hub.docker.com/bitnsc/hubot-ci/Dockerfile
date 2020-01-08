FROM node:argon

# Setup timezone
RUN echo Asia/Shanghai > /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata

# Setup locale
ENV LC_ALL C.UTF-8

# Setup tini
ENV TINI_VERSION v0.8.4
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini
ENTRYPOINT ["/tini", "--"]

# Setup hubot
RUN mkdir /opt/hubot
WORKDIR /opt/hubot

RUN npm install -g hubot coffee-script yo generator-hubot

RUN useradd -ms /bin/bash node
RUN chown -R node /opt/hubot
USER node

RUN yo hubot --owner="Bot Wrangler" --name="Hubot" --description="Delightfully aware robutt" --adapter=slack --defaults --allow-root

RUN npm install hubot-slack
RUN npm install hubot-urban
RUN npm install hubot-jenkins
RUN npm install hubot-jenkins-slack

ADD external-scripts.json /opt/hubot/external-scripts.json

# override to set proper hubot slack integration token (see slack integrations)
ENV HUBOT_SLACK_TOKEN=xxxxxxxxxxxxxxxxxxxx

CMD ["./bin/hubot", "--adapter", "slack"]

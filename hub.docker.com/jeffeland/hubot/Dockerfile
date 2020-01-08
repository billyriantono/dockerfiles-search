FROM node:11-alpine
MAINTAINER Jean-Francois Landreau

# Environment variables
ENV HUBOT_ADAPTER slack
ENV HUBOT_SLACK_TOKEN to specify
ENV HUBOT_NAME JFL-Hubot
ENV HUBOT_OWNER Jean-Francois Landreau
ENV HUBOT_DESCRIPTION Hubot for JFL

RUN addgroup -g 1001 -S hubot \
    && adduser -u 1001 -S hubot -G hubot \
    && mkdir -p /root/.config/configstore \
    && chmod g+rwx /root /root/.config /root/.config/configstore \
    && chown root:root /root/.config/ -R \
    && npm install -g yo generator-hubot --allow-root \
    && mkdir -p /home/hubot/.config/configstore \
    && echo "optOut: true" > /home/hubot/.config/configstore/insight-yo.yml \
    && mkdir -p /home/hubot/bot \
    && chown -R hubot:hubot /home/hubot

USER hubot
WORKDIR /home/hubot/bot
ADD --chown=hubot startup.sh /home/hubot/bot

RUN /usr/local/bin/yo hubot --adapter ${HUBOT_ADAPTER} --owner ${HUBOT_OWNER} --name ${HUBOT_NAME} --description ${HUBOT_DESCRIPTION} --defaults --no-insight \
    && chmod -R a+rwx /home/hubot \
    && rm /home/hubot/bot/external-scripts.json \
    && rm /home/hubot/bot/hubot-scripts.json \
    && rm /home/hubot/bot/scripts/example.coffee

ENTRYPOINT sh startup.sh

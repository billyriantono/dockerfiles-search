FROM christopotamus/hubot-docker-base

ADD . /opt/bot/

RUN npm install

ENV HUBOT_PORT 8080
ENV HUBOT_ADAPTER slack
ENV HuBOT_NAME mitec_bot
ENV HUBOT_SLACK_TOKEN ${SLACK_TOKEN}
ENV HUBOT_SLACK_TEAM mitecweb
ENV HUBOT_SLACK_BOTNAME mitec_bot
ENV PORT ${HUBOT_PORT}

CMD ["bin/hubot"]

FROM node:0.12.11
MAINTAINER Romain Commandé <commande.romain@gmail.com>

RUN npm install -g yo generator-hubot && useradd hubot -m -s /bin/sh

USER hubot
WORKDIR /home/hubot

ENV HUBOT_NAME matterbot
ENV HUBOT_OWNER someone
ENV HUBOT_DESCRIPTION hubot in mattermost
RUN echo no | yo hubot --adapter=matteruser --name=$HUBOT_NAME --owner=$HUBOT_OWNER --description=$HUBOT_DESCRIPTION && \
sed -i /heroku/d ./external-scripts.json

ENV MATTERMOST_HOST=
ENV MATTERMOST_GROUP=
ENV MATTERMOST_USER=
ENV MATTERMOST_PASSWORD=
ENV MATTERMOST_WSS_PORT=
ENV MATTERMOST_HTTP_PORT=
ENV MATTERMOST_TLS_VERIFY=
ENV MATTERMOST_USE_TLS=
ENV MATTERMOST_LOG_LEVEL=

EXPOSE 8080

ENTRYPOINT ["bin/hubot"]
CMD ["-a", "matteruser"]

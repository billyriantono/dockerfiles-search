FROM alpine:latest

LABEL vendor="Dr.Entrega" \
      maintainer="Dr.Entrega <technology+docker@drentrega.com>" \
      image="alpine" \
      tag="latest"

ENV DOCKER_HUB_URL="https://registry.hub.docker.com" \
    PLUGIN_ORGANIZATION="acme" \
    PLUGIN_REPOSITORY="my-repository" \
    DOCKER_HUB_TOKEN="secret"

RUN apk add --no-cache curl \
  && rm -rf /tmp/* /var/cache/apk/* \
  && echo $'#!/usr/bin/env sh\n \
\n \
sign () {\n \
  echo "$1"\n \
  curl -X POST --progress-bar --user-agent "drentrega/drone-plugin-docker-hub-trigger" $1\n \
  exit 0\n \
}\n \
\n \
# v2\n \
if [ ! -z $PLUGIN_URI ]; then sign $PLUGIN_URI; fi\n \
if [ ! -z $DRONE_HUB_URI ]; then sign $DRONE_HUB_URI; fi\n \
\n \
# v1\n \
sign $DOCKER_HUB_URL/u/$PLUGIN_ORGANIZATION/$PLUGIN_REPOSITORY/trigger/$(if [ ! -z $PLUGIN_TOKEN ]; then echo ${PLUGIN_TOKEN}; else echo ${DOCKER_HUB_TOKEN}; fi)/\n \
' > /ping \
  && chmod +x /ping

CMD ["sh", "-c", "/ping"]

# This dockerfile was auto-generated at 2019-01-10T11:38:35-02:00.

# In case of security branches, please contact technology+security@drentrega.com.
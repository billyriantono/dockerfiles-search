FROM skazuki/alpine-node

LABEL maintainer="S-Kazuki<contact@revoneo.com>"

ENV APP_ROOT=/node

WORKDIR $APP_ROOT

RUN npm i -g yarn \
  && npm cache clean --force

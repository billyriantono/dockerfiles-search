FROM node:8.15.1-alpine

LABEL maintainer="かとまさ <katomasa@kidding-kid.com>" \
      version="1.0.1" \
      description="Vue container." \
      registry="dockerhub" \
      app="vue-cli"

WORKDIR /app

RUN apk update && \
    npm install -g npm && \
    npm install -g @vue/cli

CMD ["/bin/sh"]
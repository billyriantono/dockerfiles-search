FROM node:11.4.0-alpine

ARG HEROKU_VERSION=7.19.3
RUN \
    apk add --update bash coreutils && \
    npm install -g heroku@$HEROKU_VERSION && \
    rm -rf /var/cache/apk/*

CMD ["bash"]


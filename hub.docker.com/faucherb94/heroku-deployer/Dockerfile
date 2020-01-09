FROM node:10.5-alpine
LABEL maintainer Ben Faucher <faucher.benp@gmail.com>

ENV HEROKU_CLI_VERSION '7.5.1'
RUN apk -U --no-cache add git && \
    npm i -g heroku@${HEROKU_CLI_VERSION}

ENTRYPOINT [ "/bin/sh", "-c" ]
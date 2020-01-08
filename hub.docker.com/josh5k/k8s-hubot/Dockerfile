FROM node:10.15-alpine

RUN npm install -g hubot@2.6.0 coffee-script redis

RUN apk update && apk upgrade && \
    apk add --no-cache bash git openssh

# Required for node-gyp to build
RUN apk add --no-cache python build-base # build base includes g++ and gcc and Make

ENV PORT 8080
EXPOSE 8080

COPY . /home/hubot

WORKDIR /home/hubot

ENTRYPOINT ["/home/hubot/bin/hubot", "-a", "slack"]
CMD ["-n", "hubot"]

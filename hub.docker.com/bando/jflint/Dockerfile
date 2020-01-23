FROM node:7-alpine

MAINTAINER "bando-shintaro" <bando142141@gmail.com>

ENV JFLINT_VERSION=0.2.0
ENV JFLINT_DIR /jflint

RUN npm install -g jflint@$JFLINT_VERSION

VOLUME $JFLINT_DIR
WORKDIR $JFLINT_DIR

ENTRYPOINT ["jflint"]

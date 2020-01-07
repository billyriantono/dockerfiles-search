FROM circleci/node:8.10
MAINTAINER jandersonfc

USER root

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
    && apt-get install -y default-jre

RUN npm install -g serverless

expose 8000
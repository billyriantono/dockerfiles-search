FROM node:alpine

RUN apk --update add openjdk8 maven python py-pip zip
RUN pip install --upgrade pip
RUN pip install awscli --upgrade --user
RUN npm install -g heroku
RUN heroku plugins:install heroku-cli-deploy

ENV PATH="/root/.local/bin:${PATH}"
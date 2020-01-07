FROM node:argon

MAINTAINER Bizmate <diego_gullo@bizmate.biz>

WORKDIR /
COPY package.json /
RUN npm install -g gulp-cli && npm install -g jspm@beta && \
    npm install
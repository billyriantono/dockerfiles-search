ARG NODE_VERSION=10.4.1
FROM node:$NODE_VERSION
MAINTAINER Michal Kordulewski <michal@kordulewski.pl>

ARG NG_CLI_VERSION=6.0.8
ARG WEBPACK_VERSION=4.12.0
ARG WEBPACK_CLI_VERSION=3.0.8
ARG GULP_VERSION=3.9.1
ARG BOWER_VERSION=1.8.4

RUN npm install -g @angular/cli@$NG_CLI_VERSION
RUN npm install -g webpack@$WEBPACK_VERSION
RUN npm install -g webpack-cli@$WEBPACK_CLI_VERSION
RUN npm install -g gulp@$GULP_VERSION
RUN npm install -g bower@$BOWER_VERSION

CMD ["bash"]
# ----- Dockerfile to build mypost-ng-cli as a base container
# docker build {--build-arg NG_CLI_VERSION=1.6.6} -t mypost-ng-cli .

FROM node:8

LABEL name="mypost-ng-cli" \
      maintainer="DDCTeamWookie <DLDDCTeamWookie@auspost.com.au>" \
      version="1.0" \
      description="The base docker container for MyPost Consumer automated testing"

ENV TZ="/usr/share/zoneinfo/Australia/Melbourne"
ENV LANG C.UTF-8
ENV NPM_CONFIG_LOGLEVEL warn

ARG NG_CLI_VERSION=1.6.6
ARG USER_HOME_DIR="/tmp"
ARG APP_DIR="/app"
ARG USER_ID=1000

ENV HOME "$USER_HOME_DIR"

RUN set -xe \
    && curl -sL https://github.com/Yelp/dumb-init/releases/download/v1.2.0/dumb-init_1.2.0_amd64 > /usr/bin/dumb-init \
    && chmod +x /usr/bin/dumb-init \
    && mkdir -p $USER_HOME_DIR \
    && chown $USER_ID $USER_HOME_DIR \
    && chmod a+rw $USER_HOME_DIR \
    && chown -R node /usr/local/lib /usr/local/include /usr/local/share /usr/local/bin \
    && (cd "$USER_HOME_DIR"; su node -c "npm i -g @angular/cli@$NG_CLI_VERSION; npm i -g yarn; npm i -g gyp node-gyp; npm cache clean --force")

WORKDIR $APP_DIR
EXPOSE 4200

ENTRYPOINT ["/usr/bin/dumb-init", "--"]

USER $USER_ID

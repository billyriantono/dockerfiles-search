# Build:
# $> docker build -t ng-cli .
# or with different cli version
# $> docker build --build-arg NG_CLI_VERSION=v1.0.1 -t ng-cli .

FROM node:7

MAINTAINER ipunkt Business Solutions OHG "info@ipunkt.biz"

ARG NG_CLI_VERSION=v1.2.0
ARG USER_HOME_DIR="/app"
ARG USER_ID=1000

ENV NPM_CONFIG_LOGLEVEL warn

RUN set -xe \
    && curl -sL https://github.com/Yelp/dumb-init/releases/download/v1.2.0/dumb-init_1.2.0_amd64 > /usr/bin/dumb-init \
    && chmod +x /usr/bin/dumb-init \
    && mkdir -p $USER_HOME_DIR \
    && chown $USER_ID $USER_HOME_DIR \
    && chmod a+rw $USER_HOME_DIR \
    && mkdir -p /.npm \
    && chown -R $USER_ID /.npm \
    && chmod -R a+rw /.npm \
    && (cd "$USER_HOME_DIR"; npm install -g @angular/cli@$NG_CLI_VERSION; npm cache clean)

VOLUME "$USER_HOME_DIR/"
WORKDIR $USER_HOME_DIR
EXPOSE 4200

ENTRYPOINT ["/usr/bin/dumb-init", "--"]

USER $USER_ID

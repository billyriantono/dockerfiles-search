FROM alpine:3.9.3

ARG NODEJS_VERSION=10.14.2-r0
ARG MODULE_VERSION=1.17.0

RUN set -x && \
    apk add --no-cache nodejs=${NODEJS_VERSION} nodejs-npm=${NODEJS_VERSION} && \
    npm install -g prettier@${MODULE_VERSION} && \
    npm install -g onchange && \
    npm cache clean --force && \
    apk del nodejs-npm

WORKDIR /work
ENTRYPOINT ["/usr/bin/onchange"]
CMD [ "**/*.html -- prettier --write {{changed}}" ]
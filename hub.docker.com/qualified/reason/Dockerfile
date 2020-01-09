FROM node:10.15.1-alpine

RUN set -ex; \
    adduser -D codewarrior; \
    ln -s /home/codewarrior /workspace;

ENV NPM_CONFIG_LOGLEVEL=warn
COPY --chown=codewarrior:codewarrior rootfs/workspace/reason/package.json /workspace/reason/package.json
COPY --chown=codewarrior:codewarrior rootfs/workspace/reason/package-lock.json /workspace/reason/package-lock.json

RUN set -ex; \
    apk add --no-cache --virtual .build-deps \
        su-exec \
        bash \
        build-base \
        python \
    ; \
    cd /workspace/reason; \
    su-exec codewarrior npm install; \
    apk del .build-deps; \
    rm -rf /home/codewarrior/.npm;

COPY --chown=codewarrior:codewarrior rootfs/workspace/reason /workspace/reason
COPY rootfs/opt/runner /opt/runner

USER codewarrior
WORKDIR /workspace
ENV USER=codewarrior HOME=/home/codewarrior NODE_ENV=production

RUN set -ex; \
    cd /workspace/reason; \
    npm run test; \
    rm -rf __tests__/* src/* lib;


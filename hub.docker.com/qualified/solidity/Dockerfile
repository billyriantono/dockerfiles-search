FROM node:10.14.0-alpine
# Truffle 5.0.3 (solc 0.5.0)

RUN set -ex; \
    adduser -D codewarrior; \
    ln -s /home/codewarrior /workspace;

ENV NPM_CONFIG_LOGLEVEL=warn
COPY --chown=codewarrior:codewarrior rootfs/workspace/solidity/package.json /workspace/solidity/package.json
COPY --chown=codewarrior:codewarrior rootfs/workspace/solidity/package-lock.json /workspace/solidity/package-lock.json

RUN set -ex; \
    apk add --no-cache --virtual .build-deps \
# su-exec makes running commands as a different user easy
        su-exec \
        bash \
        build-base \
        git \
        python \
    ; \
    cd /workspace/solidity; \
    su-exec codewarrior npm install; \
    apk del --purge .build-deps; \
    rm -rf /var/cache/apk/* /tmp/* /home/codewarrior/.npm;

USER codewarrior
COPY --chown=codewarrior:codewarrior rootfs/workspace/solidity /workspace/solidity
WORKDIR /workspace/solidity
ENV NODE_ENV=production
RUN set -ex; \
    npx truffle test; \
    rm contracts/*.sol; \
    rm test/*.js;

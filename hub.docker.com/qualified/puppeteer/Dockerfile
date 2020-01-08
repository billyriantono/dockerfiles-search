FROM node:10.16.1-alpine

RUN set -ex; \
    adduser -D codewarrior; \
    mkdir /workspace; \
    chown codewarrior:codewarrior /workspace;

RUN npm install -g pnpm@3

COPY --chown=codewarrior:codewarrior rootfs/opt/runner/jest-reporter/package.json /opt/runner/jest-reporter/package.json
COPY --chown=codewarrior:codewarrior rootfs/opt/runner/jest-reporter/pnpm-lock.yaml /opt/runner/jest-reporter/pnpm-lock.yaml

COPY --chown=codewarrior:codewarrior rootfs/workspace/puppeteer/package.json /workspace/puppeteer/package.json
COPY --chown=codewarrior:codewarrior rootfs/workspace/puppeteer/pnpm-lock.yaml /workspace/puppeteer/pnpm-lock.yaml

ENV CHROMIUM_BIN="/usr/bin/chromium-browser"
RUN set -ex; \
    apk add --no-cache --virtual .build-deps \
        bash \
        build-base \
        python \
        su-exec \
    ; \
    apk add --no-cache \
        udev \
        ttf-freefont \
        chromium \
    ; \
    cd /opt/runner/jest-reporter; \
    su-exec codewarrior pnpm install --frozen-lockfile; \
    cd /workspace/puppeteer; \
    su-exec codewarrior pnpm install --frozen-lockfile; \
    apk del .build-deps; \
    rm -rf /usr/include /var/cache/apk/* /home/codewarrior/.node-gyp /usr/share/man /tmp/*;

COPY --chown=codewarrior:codewarrior rootfs/workspace/puppeteer /workspace/puppeteer
COPY rootfs/opt/runner /opt/runner/

USER codewarrior

RUN set -ex; \
    cd /workspace/puppeteer; \
    pnpm install -D file:/opt/runner/jest-reporter;

ENV TEST_BASE_URL="http://localhost:1234" PARCEL_WORKERS=1
WORKDIR /workspace/puppeteer

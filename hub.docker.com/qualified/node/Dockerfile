FROM node:10.15.3-alpine

RUN set -ex; \
    adduser -D codewarrior -u 9999; \
    ln -s /home/codewarrior /workspace;

RUN npm install -g pnpm@3

COPY --chown=codewarrior:codewarrior rootfs/opt/runner/cw-2/package.json /opt/runner/cw-2/package.json
COPY --chown=codewarrior:codewarrior rootfs/opt/runner/cw-2/pnpm-lock.yaml /opt/runner/cw-2/pnpm-lock.yaml
COPY --chown=codewarrior:codewarrior rootfs/opt/runner/jest-reporter/package.json /opt/runner/jest-reporter/package.json
COPY --chown=codewarrior:codewarrior rootfs/opt/runner/jest-reporter/pnpm-lock.yaml /opt/runner/jest-reporter/pnpm-lock.yaml
COPY --chown=codewarrior:codewarrior rootfs/workspace/react/package.json /workspace/react/package.json
COPY --chown=codewarrior:codewarrior rootfs/workspace/react/pnpm-lock.yaml /workspace/react/pnpm-lock.yaml
COPY --chown=codewarrior:codewarrior rootfs/workspace/node/package.json /workspace/node/package.json
COPY --chown=codewarrior:codewarrior rootfs/workspace/node/pnpm-lock.yaml /workspace/node/pnpm-lock.yaml
COPY --chown=codewarrior:codewarrior rootfs/workspace/vue/package.json /workspace/vue/package.json
COPY --chown=codewarrior:codewarrior rootfs/workspace/vue/pnpm-lock.yaml /workspace/vue/pnpm-lock.yaml
COPY --chown=codewarrior:codewarrior rootfs/workspace/crypto/package.json /workspace/crypto/package.json
COPY --chown=codewarrior:codewarrior rootfs/workspace/crypto/pnpm-lock.yaml /workspace/crypto/pnpm-lock.yaml

RUN set -ex; \
    apk add --no-cache --virtual .build-deps \
# su-exec makes running commands as a different user easy
        su-exec \
        bash \
        build-base \
        python \
    ; \
    cd /opt/runner/cw-2; \
    su-exec codewarrior pnpm install --frozen-lockfile; \
    cd /opt/runner/jest-reporter; \
    su-exec codewarrior pnpm install --frozen-lockfile; \
    cd /workspace/react; \
    su-exec codewarrior pnpm install --frozen-lockfile; \
    cd /workspace/vue; \
    su-exec codewarrior pnpm install --frozen-lockfile; \
    cd /workspace/node; \
    su-exec codewarrior pnpm install --frozen-lockfile; \
    cd /workspace/crypto; \
    su-exec codewarrior pnpm install --frozen-lockfile; \
    apk del .build-deps;

USER codewarrior
COPY --chown=codewarrior:codewarrior rootfs/workspace/react /workspace/react/
COPY --chown=codewarrior:codewarrior rootfs/workspace/vue /workspace/vue/
COPY --chown=codewarrior:codewarrior rootfs/workspace/node /workspace/node/
COPY --chown=codewarrior:codewarrior rootfs/workspace/crypto /workspace/crypto/
COPY rootfs/opt/runner /opt/runner/

RUN set -ex; \
    cd /workspace/node; \
    pnpm install -D file:/opt/runner/cw-2; \
    pnpm install -D file:/opt/runner/jest-reporter; \
    cd /workspace/react; \
    pnpm install -D file:/opt/runner/jest-reporter; \
    cd /workspace/vue; \
    pnpm install -D file:/opt/runner/jest-reporter;

WORKDIR /workspace

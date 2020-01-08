FROM node:10.15.1-alpine

RUN set -ex; \
    adduser -D codewarrior -u 9999; \
    ln -s /home/codewarrior /workspace;

RUN npm -g install pnpm@3

COPY --chown=codewarrior:codewarrior rootfs/opt/runner/jest-reporter/package.json /opt/runner/jest-reporter/package.json
COPY --chown=codewarrior:codewarrior rootfs/opt/runner/jest-reporter/pnpm-lock.yaml /opt/runner/jest-reporter/pnpm-lock.yaml
COPY --chown=codewarrior:codewarrior rootfs/workspace/ts/package.json /workspace/ts/package.json
COPY --chown=codewarrior:codewarrior rootfs/workspace/ts/pnpm-lock.yaml /workspace/ts/pnpm-lock.yaml
COPY --chown=codewarrior:codewarrior rootfs/workspace/react/package.json /workspace/react/package.json
COPY --chown=codewarrior:codewarrior rootfs/workspace/react/pnpm-lock.yaml /workspace/react/pnpm-lock.yaml
COPY --chown=codewarrior:codewarrior rootfs/workspace/angular/package.json /workspace/angular/package.json
COPY --chown=codewarrior:codewarrior rootfs/workspace/angular/pnpm-lock.yaml /workspace/angular/pnpm-lock.yaml

RUN set -ex; \
    apk add --no-cache --virtual .build-deps \
# su-exec makes running commands as a different user easy
        su-exec \
    ; \
    cd /opt/runner/jest-reporter; \
    su-exec codewarrior pnpm install --frozen-lockfile; \
    cd /workspace/ts; \
    su-exec codewarrior pnpm install --frozen-lockfile; \
    cd /workspace/react; \
    su-exec codewarrior pnpm install --frozen-lockfile; \
    cd /workspace/angular; \
    su-exec codewarrior pnpm install --frozen-lockfile; \
    apk del .build-deps;

USER codewarrior
COPY rootfs/opt/runner /opt/runner
COPY --chown=codewarrior:codewarrior rootfs/workspace/ts/tsconfig.json /workspace/ts/tsconfig.json
COPY --chown=codewarrior:codewarrior rootfs/workspace/react/tsconfig.json /workspace/react/tsconfig.json
COPY --chown=codewarrior:codewarrior rootfs/workspace/angular /workspace/angular
RUN set -ex; \
    cd /workspace/ts; \
    pnpm install -D file:/opt/runner/jest-reporter; \
    cd /workspace/react; \
    pnpm install -D file:/opt/runner/jest-reporter; \
    cd /workspace/angular; \
    pnpm install -D file:/opt/runner/jest-reporter;

WORKDIR /workspace

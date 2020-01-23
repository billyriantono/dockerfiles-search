FROM node:10-alpine

MAINTAINER Krisztian Kurucz <kurucz@4dsoft.hu>

# YARN cannot be installed until the below issue will be resolved
# https://github.com/alpinelinux/aports/pull/714
RUN \
  apk add --update-cache curl git zip bash python jq openssh &&\
  npm install -g mkdirp pnpm &&\
  rm -rf \
    /usr/share/man /tmp/* /var/cache/apk/* /root/.npm /root/.node-gyp /root/.gnupg \
    /usr/lib/node_modules/npm/man /usr/lib/node_modules/npm/doc /usr/lib/node_modules/npm/html

ENTRYPOINT ["/bin/bash"]

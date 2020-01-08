FROM node:12.7-alpine
LABEL maintainer="Akira Koyasu <mail@akirakoyasu.net>"

ARG VUE_CLI_VERSION=3.9.3

USER node
RUN yarn global add @vue/cli@${VUE_CLI_VERSION}
COPY docker-entrypoint.sh /usr/local/bin/
ENV PATH="${PATH}:/home/node/.yarn/bin"

CMD vue

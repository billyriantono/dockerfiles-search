FROM node:10-alpine

RUN set -x && \
  apk update && \
  yarn global add -g npm && \
  yarn global add @vue/cli

EXPOSE 3000

CMD ["/bin/ash"]

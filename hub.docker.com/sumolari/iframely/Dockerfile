FROM node:10-alpine

EXPOSE 8061

COPY . /iframely

WORKDIR /iframely

RUN DEPS="libkrb5-dev" \
  apk --no-cache add $DEPS && \
  yarn global add forever && \
  yarn install --frozen-lockfile && \
  apk del $DEPS

ENTRYPOINT ["/iframely/docker/entrypoint.sh"]

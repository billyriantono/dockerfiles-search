FROM node:alpine

RUN apk add --no-cache git \
  && npm i -g swagger-cli redoc-cli \
  && apk del git \
  && npm cache clean -f \
  && swagger-cli --version \
  && redoc-cli --version

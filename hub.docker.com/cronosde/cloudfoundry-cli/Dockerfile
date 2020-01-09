FROM alpine

RUN apk update \
  && apk add curl \
  && curl -L "https://packages.cloudfoundry.org/stable?release=linux64-binary&source=github" | tar -zx \
  && mv cf /usr/local/bin
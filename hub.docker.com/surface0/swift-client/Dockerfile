FROM alpine:3.10

LABEL maintainer="surface0 <surface0@rainorshine.asia>"

RUN set -eux && \
  apk add --no-cache python3 && \
  apk add --virtual build-dependencies python3-dev musl-dev linux-headers gcc && \
  pip3 install python-swiftclient python-keystoneclient && \
  apk del --purge build-dependencies

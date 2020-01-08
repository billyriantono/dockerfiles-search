FROM python:3-alpine3.9

RUN set -x \
  && apk add -q --update --clean-protected --no-cache --virtual .build-deps \
     build-base \
     gcc \
     libffi-dev \
     libressl-dev \
     make \
     libgcc \
  && pip3 install ansible \
     ansible-lint \
     jinja2 \
     PyYAML \
     cryptography \
  && apk add openssh \
  && apk del .build-deps \
  && rm -rf /var/cache/apk/*

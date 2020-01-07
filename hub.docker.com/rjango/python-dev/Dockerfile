ARG PYTHON_VERSION=3.7.3
ARG ALPINE_VERSION=3.9

FROM registry.gitlab.com/rjango/images/python:$PYTHON_VERSION-alpine$ALPINE_VERSION

RUN apk add --no-cache --virtual dev-dependencies gcc musl-dev libffi-dev openssl-dev make build-base \
python3-dev git openssh openssl-dev

FROM gitlab/gitlab-runner:alpine

RUN apk update && apk upgrade && \
  apk add --no-cache \
  docker=18.06.1-r0 \
  curl \
  python

RUN python -m ensurepip && \
  rm -r /usr/lib/python*/ensurepip && \
  pip install --upgrade pip setuptools && \
  pip install docker-compose && \
  rm -r /root/.cache

RUN adduser gitlab-runner docker
RUN adduser gitlab-runner ping


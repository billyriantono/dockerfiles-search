FROM node:alpine
RUN apk update && \
  apk add --no-cache docker py-pip make python-dev libffi-dev openssl-dev gcc libc-dev && \
  pip install docker-compose

COPY Dockerfile /Dockerfile
LABEL org.label-schema.docker.dockerfile="/Dockerfile" \
  org.label-schema.vcs-type="Git" \
  org.label-schema.vcs-url="https://github.com/alersrt/node-dind"

ENTRYPOINT ["/sbin/tini", "--"]

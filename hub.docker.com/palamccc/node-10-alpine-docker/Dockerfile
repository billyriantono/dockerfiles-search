FROM node:10-alpine
RUN apk add --no-cache wget ca-certificates git \
  && cd /tmp \
  && wget https://download.docker.com/linux/static/stable/x86_64/docker-19.03.5.tgz \
  && tar -xvf docker*.tgz \
  && mv docker/docker /usr/local/bin \
  && rm -rf /tmp/*

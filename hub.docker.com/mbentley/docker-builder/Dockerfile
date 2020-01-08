FROM alpine:3.5

RUN apk --no-cache add bash curl git make &&\
  curl https://get.docker.com/builds/Linux/x86_64/docker-17.03.1-ce.tgz > /tmp/docker-17.03.1-ce.tgz &&\
  cd /tmp &&\
  tar zxvf docker-17.03.1-ce.tgz &&\
  mv docker/docker /usr/bin/docker &&\
  rm -rf /tmp/docker-17.03.1-ce.tgz docker &&\
  apk del curl

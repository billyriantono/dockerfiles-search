FROM ubuntu:18.04

RUN apt-get update && \
  apt-get install -y curl && \
  apt-get clean

ARG version=\$latest

RUN curl -Lo /usr/bin/jfrog https://api.bintray.com/content/jfrog/jfrog-cli-go/$version/jfrog-cli-linux-amd64/jfrog?bt_package=jfrog-cli-linux-amd64

RUN chmod +x /usr/bin/jfrog

ENTRYPOINT ["/usr/bin/jfrog"]

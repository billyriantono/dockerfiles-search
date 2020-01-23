FROM alpine:3.5
MAINTAINER Arthur Axel fREW Schmidt <hugo@afoolishmanifesto.com>

ENTRYPOINT ["/usr/local/bin/hugo"]

WORKDIR "/tmp/pwd"
ADD ./bin/setup /usr/local/bin/setup
RUN /usr/local/bin/setup

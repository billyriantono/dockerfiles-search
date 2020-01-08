FROM debian:latest

ENV S6_RELEASE 1.21.4.0

ADD https://github.com/just-containers/s6-overlay/releases/download/v$S6_RELEASE/s6-overlay-amd64.tar.gz /tmp/
RUN tar xzf /tmp/s6-overlay-amd64.tar.gz -C /

RUN apt-get update
RUN apt-get install cowsay fortune -y

COPY install.sh /etc/cont-init.d/

ENTRYPOINT ["/init"]

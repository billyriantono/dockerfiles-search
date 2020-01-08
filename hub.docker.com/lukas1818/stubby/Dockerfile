FROM debian:stable-slim
LABEL git="https://github.com/Lukas1818/docker-stubby"

ADD . /build

RUN /build/install.sh

COPY stubby.yml /etc/stubby/

EXPOSE 53/UDP

ENTRYPOINT ["/usr/bin/stubby","-l"]

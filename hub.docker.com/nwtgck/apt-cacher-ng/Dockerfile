# (base: http://docs.docker.jp/engine/examples/apt-cacher-ng.html)

FROM ubuntu:16.04
LABEL maintainer="Ryo Ota <nwtgck@gmail.com>"

RUN apt update && \
    apt install -y apt-cacher-ng

CMD chmod 777 /var/cache/apt-cacher-ng && /etc/init.d/apt-cacher-ng start && tail -f /var/log/apt-cacher-ng/*

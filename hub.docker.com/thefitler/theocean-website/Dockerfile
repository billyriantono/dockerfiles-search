FROM debian:jessie

RUN mkdir -p /data/ocean

ADD . /data/ocean

VOLUME /data/ocean

CMD /data/ocean/docker-entrypoint.sh

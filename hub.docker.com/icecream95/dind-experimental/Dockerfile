FROM docker:dind
MAINTAINER Icecream95

RUN mkdir -p /etc/docker; echo "{\"experimental\": true}" >> /etc/docker/daemon.json

VOLUME /var/lib/docker
EXPOSE 2375

ENTRYPOINT ["dockerd-entrypoint.sh"]
CMD []

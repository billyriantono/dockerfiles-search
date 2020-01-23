FROM openjdk:8-jre-alpine

RUN mkdir -p /opt/docker

ADD docker-entrypoint.sh /opt/docker

ENTRYPOINT ["/opt/docker/docker-entrypoint.sh"]

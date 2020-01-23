FROM openjdk:8-jre-alpine
MAINTAINER Daniel Liljeberg <liljebergxyz@gmail.com>

ARG ELASTICMQ_VERSION
ENV ELASTICMQ_VERSION ${ELASTICMQ_VERSION:-0.14.6}

RUN apk add --no-cache curl ca-certificates bash
RUN mkdir -p /elasticmq/log /elasticmq/lib /elasticmq/config
RUN curl -sfLo /elasticmq/elasticmq.jar https://s3-eu-west-1.amazonaws.com/softwaremill-public/elasticmq-server-${ELASTICMQ_VERSION}.jar

WORKDIR /elasticmq

EXPOSE 9324

COPY resources/entrypoint.sh /usr/bin/
COPY resources/base.conf /elasticmq/

ENTRYPOINT ["entrypoint.sh"]
CMD ["/usr/bin/java", "-Dconfig.file=custom.conf", "-jar", "/elasticmq/elasticmq.jar"]

FROM alpine:latest as builder
MAINTAINER Paul Nigsch

RUN apk add --no-cache curl
WORKDIR /opt
RUN curl -O https://d3kbcqa49mib13.cloudfront.net/spark-2.2.0-bin-hadoop2.7.tgz
#COPY spark-2.2.0-bin-hadoop2.7.tgz .
RUN tar xzf spark-2.2.0-bin-hadoop2.7.tgz
RUN rm  spark-2.2.0-bin-hadoop2.7.tgz



FROM openjdk:8-jre-alpine as final
MAINTAINER Paul Nigsch

COPY --from=builder /opt/spark-2.2.0-bin-hadoop2.7/ /opt/spark-2.2.0

WORKDIR /opt/spark-2.2.0
RUN apk add --update bash bind-tools python  && rm -rf /var/cache/apk/*

CMD ["/bin/bash"] 


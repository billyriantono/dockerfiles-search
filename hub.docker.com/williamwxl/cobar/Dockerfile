FROM openjdk:8-jre-slim

ARG cobar_version=1.2.7

MAINTAINER WilliamWei

ENV COBAR_VERSION=$cobar_version \
    COBAR_HOME=/opt/cobar \

ENV PATH=${PATH}:${COBAR_HOME}/bin

RUN apt-get update && \
    apt-get install -y wget && \
    wget https://github.com/alibaba/cobar/releases/download/v${COBAR_VERSION}/cobar-server-${COBAR_VERSION}.tar.gz && \
    mkdir /opt/cobar && \
    tar -zxvf cobar-server-${COBAR_VERSION}.tar.gz -C /opt/cobar && \
    rm cobar-server-${COBAR_VERSION}.tar.gz && \
    cd /opt/cobar

WORKDIR /opt/cobar

VOLUME /opt/cobar/conf

CMD ["./startup.sh"]
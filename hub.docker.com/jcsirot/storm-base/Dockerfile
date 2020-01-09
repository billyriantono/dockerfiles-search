FROM fedora:latest

MAINTAINER Jean-Christophe Sirot <jc@sirot.org>

ARG VERSION=1.0.0

RUN yum update -y && yum install -y java python tar

RUN curl -s http://archive.apache.org/dist/storm/apache-storm-$VERSION/apache-storm-$VERSION.tar.gz | \
    tar zxf - -C /opt && \
    mv /opt/apache-storm-$VERSION /opt/apache-storm

WORKDIR /opt/apache-storm

ENTRYPOINT ["bin/storm"]

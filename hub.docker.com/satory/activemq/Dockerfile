FROM java:7
MAINTAINER John McDonnell <john.mcdonnell@bearingpoint.com>


ENV ACTIVEMQ_VERSION 5.13.0
ENV ACTIVEMQ apache-activemq-$ACTIVEMQ_VERSION

ENV ACTIVEMQ_HOME /opt/$ACTIVEMQ

RUN \
    curl -O http://archive.apache.org/dist/activemq/$ACTIVEMQ_VERSION/$ACTIVEMQ-bin.tar.gz && \
    mkdir -p /opt && \
    tar xf $ACTIVEMQ-bin.tar.gz -C /opt/ && \
    rm $ACTIVEMQ-bin.tar.gz 


WORKDIR $ACTIVEMQ_HOME
EXPOSE 61616 8161

CMD bin/activemq console

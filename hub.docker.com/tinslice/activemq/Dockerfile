FROM adoptopenjdk/openjdk11:alpine-slim

ENV ACTIVEMQ_VERSION 5.15.10
ENV ACTIVEMQ apache-activemq-$ACTIVEMQ_VERSION
ENV ACTIVEMQ_UI=8161 ACTIVEMQ_TCP=61616 ACTIVEMQ_MQTT=1883 ACTIVEMQ_AMQP=5672 ACTIVEMQ_STOMP=61613 ACTIVEMQ_WS=61614 

ENV ACTIVEMQ_HOME /opt/activemq

RUN mkdir -p /opt && \
    apk add --update --no-cache \
            tar \
            bash \
            wget && \
    wget https://archive.apache.org/dist/activemq/$ACTIVEMQ_VERSION/$ACTIVEMQ-bin.tar.gz

RUN tar -xzvf $ACTIVEMQ-bin.tar.gz -C /opt && \
    ln -s /opt/$ACTIVEMQ $ACTIVEMQ_HOME && \
    mkdir -p /opt/template/activemq && \
    cp -r /opt/$ACTIVEMQ/conf /opt/template/activemq/ && \
    cp -r /opt/$ACTIVEMQ/data /opt/template/activemq/ && \
    addgroup -S activemq && \
    adduser -S -G activemq --home ${ACTIVEMQ_HOME} activemq && \
    chown -R activemq:activemq /opt/$ACTIVEMQ && \
    chown -h activemq:activemq $ACTIVEMQ_HOME && \
    chown -h activemq:activemq /opt/template/activemq

COPY fs/ /

RUN chmod +x /prepare-env-and-run.sh && \ 
    chown activemq:activemq /prepare-env-and-run.sh

USER activemq

WORKDIR $ACTIVEMQ_HOME
EXPOSE $ACTIVEMQ_UI $ACTIVEMQ_TCP $ACTIVEMQ_MQTT $ACTIVEMQ_AMQP $ACTIVEMQ_STOMP $ACTIVEMQ_WS 

CMD ["/bin/sh", "-c", "/prepare-env-and-run.sh"]

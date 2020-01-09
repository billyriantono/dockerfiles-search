FROM openjdk:8-jre-alpine

ENV ACTIVEMQ_VERSION 5.15.10
ENV ACTIVEMQ_DIST=apache-activemq-$ACTIVEMQ_VERSION \
    ACTIVEMQ_HOME=/usr/local/activemq \
    ACTIVEMQ_BASE=/usr/local/activemq \
    ACTIVEMQ_CONF=/usr/local/activemq/conf \
    ACTIVEMQ_DATA=/usr/local/activemq/data

RUN  wget -O activemq.tar.gz \
        https://archive.apache.org/dist/activemq/${ACTIVEMQ_VERSION}/${ACTIVEMQ_DIST}-bin.tar.gz && \
    tar xzvf activemq.tar.gz -C  /usr/local && \
    ln -s /usr/local/$ACTIVEMQ_DIST $ACTIVEMQ_HOME && \
    addgroup -S activemq && adduser -S -H -G activemq -h $ACTIVEMQ_HOME activemq && \
    chown -R activemq:activemq /usr/local/$ACTIVEMQ_DIST && \
    chown -h activemq:activemq ${ACTIVEMQ_HOME} && \
    rm activemq.tar.gz

WORKDIR $ACTIVEMQ_HOME

USER activemq

COPY activemq.xml conf/

COPY run_tests.sh /

CMD ["/bin/sh", "-c", "bin/activemq console"]
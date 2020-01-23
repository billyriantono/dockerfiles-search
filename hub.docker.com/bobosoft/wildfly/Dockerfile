FROM openjdk:8-jdk-alpine

RUN apk add --no-cache curl

ENV WILDFLY_VERSION 10.1.0.Final

ENV JBOSS_HOME /opt/jboss/wildfly

ENV LAUNCH_JBOSS_IN_BACKGROUND true

RUN addgroup -g 1000 -S jboss && adduser -S jboss -G jboss -h /opt/jboss -D -u 1000 && \
    chmod 755 /opt/jboss

WORKDIR /opt/jboss

RUN cd $HOME \
    && curl -O https://download.jboss.org/wildfly/$WILDFLY_VERSION/wildfly-$WILDFLY_VERSION.tar.gz \
    && tar xf wildfly-$WILDFLY_VERSION.tar.gz \
    && mv $HOME/wildfly-$WILDFLY_VERSION $JBOSS_HOME \
    && rm wildfly-$WILDFLY_VERSION.tar.gz \
    && chown -R jboss:0 ${JBOSS_HOME} \
    && chmod -R g+rw ${JBOSS_HOME}

USER jboss

EXPOSE 8080

CMD ["/opt/jboss/wildfly/bin/standalone.sh", "-b", "0.0.0.0"]
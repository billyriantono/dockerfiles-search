FROM openjdk:8-jdk-alpine

USER root

ENV WILDFLY_VERSION 10.1.0.Final
ENV WILDFLY_HOME /opt/wf
ENV JBOSS_HOME $WILDFLY_HOME
ENV PATH $WILDFLY_HOME/bin:$PATH
ENV WILDFLY_DOWN_FILE wildfly-$WILDFLY_VERSION.tar.gz
#ENV CONFIG_FILE standalone-full.xml
#ENV CONFIG_FILE standalone.xml

RUN set -x ; \
    mkdir -p $WILDFLY_HOME ; \
    cd $WILDFLY_HOME ; \
    wget http://download.jboss.org/wildfly/$WILDFLY_VERSION/$WILDFLY_DOWN_FILE ; \
    tar -xvf $WILDFLY_DOWN_FILE --strip-components=1 ; \
    rm -rf bin/*.bat ; \
    rm -rf bin/*.ps1 ; \
    rm -rf $WILDFLY_DOWN_FILE ; \
    echo -e "\nJAVA_OPTS=\"\$JAVA_OPTS -Duser.language=pt -Duser.country=BR -Duser.timezone=America/Belem\"" >> $WILDFLY_HOME/bin/standalone.conf ; \
    chown root:root -R /opt

WORKDIR $WILDFLY_HOME

#COPY $CONFIG_FILE standalone/configuration/$CONFIG_FILE

EXPOSE 8080 9990

#CMD bin/standalone.sh --server-config=$CONFIG_FILE -b 0.0.0.0
CMD bin/standalone.sh -b=0.0.0.0 -bmanagement=0.0.0.0
FROM davimss/docker-jdk:8

ENV WILDFLY_VERSION 13.0.0.Final
ENV WILDFLY_HOME /opt/wf
ENV JBOSS_HOME $WILDFLY_HOME
ENV PATH $WILDFLY_HOME/bin:$PATH
ENV WILDFLY_DOWN_FILE wildfly-$WILDFLY_VERSION.tar.gz
ENV WILDFLY_BASE_DOWNLOAD_URL http://download.jboss.org/wildfly
ENV WILDFLY_DEPLOY_DIR ${WILDFLY_HOME}/standalone/deployments
ENV WILDFLY_CONFIG_DIR ${WILDFLY_HOME}/standalone/configuration

RUN set -x ; \
    mkdir -p $WILDFLY_HOME ; \
    cd $WILDFLY_HOME ; \
    curl -O $WILDFLY_BASE_DOWNLOAD_URL/$WILDFLY_VERSION/$WILDFLY_DOWN_FILE ; \
    tar -xvf $WILDFLY_DOWN_FILE --strip-components=1 ; \
    rm -rf bin/*.bat ; \
    rm -rf bin/*.ps1 ; \
    rm -rf $WILDFLY_DOWN_FILE ; \
    echo -e "\nJAVA_OPTS=\"\$JAVA_OPTS -Duser.language=pt -Duser.country=BR -Duser.timezone=America/Belem\"" >> $WILDFLY_HOME/bin/standalone.conf

WORKDIR $WILDFLY_HOME

COPY standalone.xml ${WILDFLY_CONFIG_DIR}
COPY ojdbc6-11.2.0.3.0.jar ${WILDFLY_DEPLOY_DIR}

# EXPOSE 8080 8443

#CMD bin/standalone.sh -b=0.0.0.0 -bmanagement=0.0.0.0
CMD bin/standalone.sh -b=0.0.0.0

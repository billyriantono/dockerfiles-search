FROM humanswitch/wildfly11:latest

ENV KEYCLOAK_ADAPTER_VERSION 3.4.3.Final
ENV KEYCLOAK_ADAPTER_FILENAME=keycloak-wildfly-adapter-dist-$KEYCLOAK_ADAPTER_VERSION.tar.gz
ENV KEYCLOAK_ADAPTER_SHA 0830872f6ddee855545b27bed32e9ac6815e484c
ENV KEYCLOAK_ADAPTER_URL https://downloads.jboss.org/keycloak/$KEYCLOAK_ADAPTER_VERSION/adapters/keycloak-oidc/${KEYCLOAK_ADAPTER_FILENAME}
USER root

RUN cd $HOME \
    && curl -O ${KEYCLOAK_ADAPTER_URL} \
    && sha1sum ${KEYCLOAK_ADAPTER_FILENAME} | grep ${KEYCLOAK_ADAPTER_SHA} \
    && tar xf ${KEYCLOAK_ADAPTER_FILENAME} -C ${JBOSS_HOME} \
    && rm ${KEYCLOAK_ADAPTER_FILENAME} \
    && ${JBOSS_HOME}/bin/jboss-cli.sh --file=${JBOSS_HOME}/bin/adapter-elytron-install-offline.cli \
    && rm -rf ${JBOSS_HOME}/standalone/configuration/standalone_xml_history/current \
    && chown -R jboss:0 ${JBOSS_HOME} \
    && chmod -R g+rw ${JBOSS_HOME}

USER jboss
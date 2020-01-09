FROM mrebscher/alpinejdk8
MAINTAINER mrebscher

ENV PAYARA_ARCHIVE=payara41
ENV DOMAIN_NAME=domain1
ENV INSTALL_DIR=/opt
ENV PAYARA_HOME=${INSTALL_DIR}/payara41/glassfish
ENV EXEC=${PAYARA_HOME}/bin
ENV DEPLOYMENT_DIR=${PAYARA_HOME}/domains/${DOMAIN_NAME}/autodeploy/
ENV PATH=${EXEC}:$PATH

RUN curl -o ${INSTALL_DIR}/${PAYARA_ARCHIVE}.zip -L http://bit.ly/1Gm0GIw && \
  unzip ${INSTALL_DIR}/${PAYARA_ARCHIVE}.zip -d /opt \
  && rm ${INSTALL_DIR}/${PAYARA_ARCHIVE}.zip

ENTRYPOINT asadmin start-domain --verbose ${DOMAIN_NAME}
WORKDIR /opt/payara41/glassfish/bin
EXPOSE 4848 8009 8080 8181

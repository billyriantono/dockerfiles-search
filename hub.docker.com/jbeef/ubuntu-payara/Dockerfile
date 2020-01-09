FROM jbeef/ubuntu-java8:latest

MAINTAINER alex

ENV PAYARA_ARCHIVE payara5
ENV DOMAIN_NAME domain1
ENV INSTALL_DIR /opt

RUN apt-get update && \
apt-get install -y curl && \
apt-get install -y unzip && \
curl -o ${INSTALL_DIR}/${PAYARA_ARCHIVE}.zip -L https://s3-eu-west-1.amazonaws.com/payara.fish/Payara+Downloads/5.181/payara-5.181.zip && \
unzip ${INSTALL_DIR}/${PAYARA_ARCHIVE}.zip -d ${INSTALL_DIR} && \
rm ${INSTALL_DIR}/${PAYARA_ARCHIVE}.zip

ENV PAYARA_HOME ${INSTALL_DIR}/${PAYARA_ARCHIVE}/glassfish
ENV DEPLOYMENT_DIR ${PAYARA_HOME}/domains/${DOMAIN_NAME}/autodeploy/

WORKDIR ${PAYARA_HOME}/bin

ENTRYPOINT asadmin start-domain ${DOMAIN_NAME} && \
tail -f ${PAYARA_HOME}/domains/${DOMAIN_NAME}/logs/server.log

EXPOSE 4848 8009 8080 8181

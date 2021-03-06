FROM openjdk:8-jre-alpine

# env vars
ENV IMAGE_VERSION 2
ENV QPID_VERSION 7.1.2
ENV QPID_ARCHIVE apache-qpid-broker-j-${QPID_VERSION}-bin.tar.gz
ENV QPID_DOWNLOAD_URL https://www-eu.apache.org/dist/qpid/broker-j/${QPID_VERSION}/binaries/${QPID_ARCHIVE}
ENV QPID_INSTALL /usr/local
ENV INITIAL_CONFIG ${QPID_INSTALL}/initial-config.json
ENV QPID_HOME ${QPID_INSTALL}/qpid-broker/${QPID_VERSION}
ENV QPID_SERVER ${QPID_HOME}/bin/qpid-server 
ENV QPID_WORK /var/qpid-work

# labels
LABEL "version"="${QPID_VERSION}-${IMAGE_VERSION}"
LABEL "qpid-version"="${QPID_VERSION}"
LABEL "description"="This image provides the Qpid Broker-J server version ${QPID_VERSION}."

# prepare system
RUN apk add --no-cache bash

# download and install qpid broker-j
WORKDIR ${QPID_INSTALL}
RUN wget ${QPID_DOWNLOAD_URL}
RUN tar -xvf ${QPID_ARCHIVE}
RUN rm ${QPID_ARCHIVE}

# volumes
VOLUME ${QPID_INSTALL}
VOLUME ${QPID_WORK}

# start qpid broker-j
ENTRYPOINT ["/usr/local/qpid-broker/7.1.2/bin/qpid-server"]
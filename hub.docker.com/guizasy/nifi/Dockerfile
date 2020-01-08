      FROM openjdk:8-jre

      ARG NIFI_VERSION=1.9.2
      ARG BASE_URL=https://archive.apache.org/dist
      ARG MIRROR_BASE_URL=${MIRROR_BASE_URL:-${BASE_URL}}
      ARG NIFI_BINARY_PATH=${NIFI_BINARY_PATH:-/nifi/${NIFI_VERSION}/nifi-${NIFI_VERSION}-bin.zip}

      ENV NIFI_BASE_DIR=/opt/nifi
      ENV NIFI_HOME=${NIFI_BASE_DIR}/nifi-current
      ENV NIFI_PID_DIR=${NIFI_HOME}/run
      ENV NIFI_LOG_DIR=${NIFI_HOME}/logs
      ENV NIFI_SCRIPTS_DIR=${NIFI_BASE_DIR}/scripts
      ENV OPENSHIFT_DEFAULT_PERMISSIONS=777

      RUN umask 000

      ADD sh/ ${NIFI_BASE_DIR}/scripts/

      # Setup NiFi user and create necessary directories
      RUN mkdir -m ${OPENSHIFT_DEFAULT_PERMISSIONS} -p ${NIFI_BASE_DIR} \
          && apt-get update \
          && apt-get install -y jq xmlstarlet procps

      # Download, validate, and expand Apache NiFi binary.
      RUN curl -fSL ${MIRROR_BASE_URL}/${NIFI_BINARY_PATH} -o ${NIFI_BASE_DIR}/nifi-${NIFI_VERSION}-bin.zip \
          && echo "$(curl ${BASE_URL}/${NIFI_BINARY_PATH}.sha256) *${NIFI_BASE_DIR}/nifi-${NIFI_VERSION}-bin.zip" | sha256sum -c - \
          && unzip ${NIFI_BASE_DIR}/nifi-${NIFI_VERSION}-bin.zip -d ${NIFI_BASE_DIR} \
          && rm ${NIFI_BASE_DIR}/nifi-${NIFI_VERSION}-bin.zip \
          && mv ${NIFI_BASE_DIR}/nifi-${NIFI_VERSION} ${NIFI_HOME} \
          && chmod -R ${OPENSHIFT_DEFAULT_PERMISSIONS} ${NIFI_HOME} \
          && chmod -R ${OPENSHIFT_DEFAULT_PERMISSIONS} ${NIFI_SCRIPTS_DIR} \
          && mkdir -m ${OPENSHIFT_DEFAULT_PERMISSIONS} -p ${NIFI_HOME}/conf \
          && mkdir -m ${OPENSHIFT_DEFAULT_PERMISSIONS} -p ${NIFI_HOME}/database_repository \
          && mkdir -m ${OPENSHIFT_DEFAULT_PERMISSIONS} -p ${NIFI_HOME}/flowfile_repository \
          && mkdir -m ${OPENSHIFT_DEFAULT_PERMISSIONS} -p ${NIFI_HOME}/content_repository \
          && mkdir -m ${OPENSHIFT_DEFAULT_PERMISSIONS} -p ${NIFI_HOME}/provenance_repository \
          && mkdir -m ${OPENSHIFT_DEFAULT_PERMISSIONS} -p ${NIFI_HOME}/state \
          && mkdir -m ${OPENSHIFT_DEFAULT_PERMISSIONS} -p ${NIFI_LOG_DIR} \
          && ln -s ${NIFI_HOME} ${NIFI_BASE_DIR}/nifi-${NIFI_VERSION}

      VOLUME ${NIFI_LOG_DIR} \
            ${NIFI_HOME}/conf \
            ${NIFI_HOME}/database_repository \
            ${NIFI_HOME}/flowfile_repository \
            ${NIFI_HOME}/content_repository \
            ${NIFI_HOME}/provenance_repository \
            ${NIFI_HOME}/state

      RUN echo "#!/bin/sh\n" > ${NIFI_HOME}/bin/nifi-env.sh

      EXPOSE 8080 8443 10000

      WORKDIR ${NIFI_HOME}

      ENTRYPOINT ["../scripts/start.sh"]

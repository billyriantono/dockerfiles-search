FROM openjdk:8-jdk-alpine

ENV PENTAHO_HOME=/data-integration
ENV PATH=$PATH:${PENTAHO_HOME}

ARG MAJOR_MINOR_VERSION=8.3
ARG VERSION=8.3.0.0-371
ENV FILENAME=pdi-ce-${VERSION}.zip
ENV URL_KETTLE=https://iweb.dl.sourceforge.net/project/pentaho/Pentaho%20${MAJOR_MINOR_VERSION}/client-tools/${FILENAME}

RUN echo ${URL_KETTLE} && wget ${URL_KETTLE} -O ${FILENAME} \
    && unzip -d / ${FILENAME} \
    && rm ${FILENAME} \
    && sed -i 's/OPT="$OPT $PENTAHO_DI_JAVA_OPTIONS/OPT="$OPT $PENTAHO_DI_JAVA_OPTIONS -Duser.timezone=GMT-3/' ${PENTAHO_HOME}/spoon.sh \
    && rm -r ${PENTAHO_HOME}/samples ${PENTAHO_HOME}/docs

FROM alpine:3.5

MAINTAINER 8 Wire Digital <info@8wiredigital.co.nz>


ENV SOLR_VERSION=3.6.2 \
    SOLR_USER=www \
    SOLR_USERID=9999 \
    SRC_DIR=/tmp/src \
    BUILD_DEPS="curl" \
    PERSISTANT_DEPS="openjdk7-jre"

#set up user
RUN adduser -D -u ${SOLR_USERID} ${SOLR_USER}

RUN apk --update add ${PERSISTANT_DEPS} ${BUILD_DEPS} \
    && mkdir -p ${SRC_DIR} \
    && curl http://archive.apache.org/dist/lucene/solr/${SOLR_VERSION}/apache-solr-${SOLR_VERSION}.tgz  > ${SRC_DIR}/solr-${SOLR_VERSION}.tgz \
    && cd ${SRC_DIR} \
    && tar -zxvf ${SRC_DIR}/solr-${SOLR_VERSION}.tgz -C ${SRC_DIR} \
    && mkdir /opt \
    && mv ${SRC_DIR}/apache-solr-${SOLR_VERSION} /opt/solr \
    && mv /opt/solr/example /opt/solr/core \
    && apk del ${BUILD_DEPS} \
    && apk add ${PERSISTANT_DEPS} \
    && rm -rf ${SRC_DIR} \
    && rm -rf /var/cache/apk/* \
    && rm -rf /opt/solr/docs

RUN ln -sf /dev/stdout /var/log/solr.log

EXPOSE 8983

WORKDIR /opt/solr/core
CMD ["java", "-jar", "start.jar"]
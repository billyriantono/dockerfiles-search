FROM quay.io/lizhongwen/oracle-jdk:1.8 
 
MAINTAINER github.com/Official-Registry, lizhongwen1989@gmail.com 

ENV ARCHIVA_HOME="/opt/app/archiva"
ENV ARCHIVA_VERSION="2.2.1"

# jvm memory limits (unit: MB)
ENV MAX_HEAP=512
ENV MIN_HEAP=512

EXPOSE 8080

VOLUME /repository

RUN curl --fail --location --retry 3 \
  http://mirror.bit.edu.cn/apache/archiva/2.2.1/binaries/apache-archiva-2.2.1-bin.tar.gz \
  -o /tmp/archiva.tar.gz \
  && tar -zvxf /tmp/archiva.tar.gz -C /tmp/ \
  && mkdir -p /opt/app/ \
  && mv /tmp/apache-archiva-${ARCHIVA_VERSION} ${ARCHIVA_HOME} \
  && rm -rf /tmp/archiva.tar.gz

ADD resources/entrypoint.sh ${ARCHIVA_HOME}/bin/

RUN chmod +x ${ARCHIVA_HOME}/bin/entrypoint.sh

ENTRYPOINT ["/bin/sh", "-c", "${ARCHIVA_HOME}/bin/entrypoint.sh"]

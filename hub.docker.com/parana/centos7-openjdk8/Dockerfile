FROM parana/centos7
# Based on centos:7.2.1511 Public Image

MAINTAINER "João Antonio Ferreira" <joao.parana@gmail.com>`

ENV REFRESHED_AT 2016-07-15

# RUN yum update -y 
RUN yum -y install unzip \
    && yum -y install java-1.8.0-openjdk-devel \
    && yum clean all

ENV JAVA_HOME /usr/lib/jvm/java-1.8.0
ENV PATH "$PATH":/${JAVA_HOME}/bin:.:

ENV DOWNLOAD_H2 http://www.h2database.com/h2-2014-04-05.zip
ENV DATA_DIR /opt/h2-data
ENV H2_VERSION 1.3.176

RUN curl ${DOWNLOAD_H2} -o h2.zip \
    && unzip h2.zip -d /usr/local/ \
    && rm h2.zip \
    && mkdir -p ${DATA_DIR}

EXPOSE 83 1521

RUN ls -la /usr/local/h2/bin \
    && ls -la / \
    && echo "java -cp /usr/local/h2/bin/h2-${H2_VERSION}.jar org.h2.tools.Server -web -webAllowOthers -webPort 83 -tcp -tcpAllowOthers -tcpPort 1521 -baseDir ${DATA_DIR}" > /start-h2.sh \
    && chmod a+rx /start-h2.sh \
    && echo "Execute /start-h2.sh para iniciar o Banco de Dados na porta 1521 "

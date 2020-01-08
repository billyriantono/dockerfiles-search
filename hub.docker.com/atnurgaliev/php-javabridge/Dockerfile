FROM ubuntu:16.04

MAINTAINER Alexey Nurgaliev <atnurgaliev@gmail.com>

ENV DEBIAN_FRONTEND=noninteractive

ENV JAVA_BRIDGE_URL="https://sourceforge.net/projects/php-java-bridge/files/Binary%20package/php-java-bridge_7.1.3/php-java-bridge_7.1.3_documentation.zip/download"

ENV JAYBIRD_URL="https://github.com/FirebirdSQL/jaybird/releases/download/v2.2.13/Jaybird-2.2.13-JDK_1.8.zip"
ENV JAYBIRD_FILE_NAME="jaybird-full-2.2.13.jar"

ENV POSTGRESQL_URL="https://jdbc.postgresql.org/download/postgresql-9.4.1212.jar"
ENV POSTGRESQL_FILE_NAME="postgresql-9.4.1212.jar"

ENV TOMCAT_URL="http://apache-mirror.rbc.ru/pub/apache/tomcat/tomcat-8/v8.5.15/bin/apache-tomcat-8.5.15.tar.gz"
ENV TOMCAT_DIR="/opt/apache-tomcat-8.5.15"
ENV TOMCAT_LIB_DIR="${TOMCAT_DIR}/webapps/JavaBridge/WEB-INF/lib"

RUN apt-get update -y && \
    apt-get upgrade -y && \
    apt-get install -y unzip wget php-cgi openjdk-8-jre-headless locales &&\
    locale-gen --lang ru_RU.UTF-8

RUN cd /opt &&\

    wget -O "tomcat.tar.gz" "${TOMCAT_URL}" &&\
    tar -xf "tomcat.tar.gz" &&\
    rm "tomcat.tar.gz" &&\

    wget -O "JavaBridge.zip" "${JAVA_BRIDGE_URL}" &&\
    unzip "JavaBridge.zip" -d "JavaBridge" &&\
    unzip -o "JavaBridge/JavaBridge.war" -d "${TOMCAT_DIR}/webapps/JavaBridge" &&\
    rm -R JavaBridge &&\
    rm JavaBridge.zip &&\

    wget -O "jaybird.zip" "${JAYBIRD_URL}" &&\
    unzip "jaybird.zip" -d "jaybird" &&\
    cp "jaybird/${JAYBIRD_FILE_NAME}" "${TOMCAT_LIB_DIR}" &&\
    rm -R "jaybird" &&\

    wget "${POSTGRESQL_URL}" &&\
    cp "${POSTGRESQL_FILE_NAME}" "${TOMCAT_LIB_DIR}" &&\
    rm "${POSTGRESQL_FILE_NAME}"

EXPOSE 8080

CMD LANG=ru_RU.UTF-8 "${TOMCAT_DIR}/bin/catalina.sh" run

FROM alpine:latest

RUN apk add --update openjdk8-jre curl bash && rm -f /var/cache/apk/*

ENV LIQUIBASE_VERSION=3.5.3 \
    LIQUIBASE_PREFIX=/usr/local/lib \
    LIQUIBASE_BIN=/usr/local/bin \
    JDBC_POSTGRES_VERSION=9.4.1212 \
    JDBC_MYSQL_VERSION=1.5.7

RUN mkdir ${LIQUIBASE_PREFIX}/liquibase
WORKDIR /usr/local/lib/liquibase
RUN curl -o /tmp/liquibase-${LIQUIBASE_VERSION}.tar.gz -sSL https://github.com/liquibase/liquibase/releases/download/liquibase-parent-${LIQUIBASE_VERSION}/liquibase-${LIQUIBASE_VERSION}-bin.tar.gz
RUN tar -zxf /tmp/liquibase-${LIQUIBASE_VERSION}.tar.gz -C ${LIQUIBASE_PREFIX}/liquibase
RUN sed -i "s|bash$|ash|" ${LIQUIBASE_PREFIX}/liquibase/liquibase
RUN chmod +x ${LIQUIBASE_PREFIX}/liquibase/liquibase

RUN ln -s ${LIQUIBASE_PREFIX}/liquibase/liquibase ${LIQUIBASE_BIN}

RUN curl -o ${LIQUIBASE_PREFIX}/liquibase/lib/mariadb-${JDBC_MYSQL_VERSION}.jar -sSL https://downloads.mariadb.com/Connectors/java/connector-java-${JDBC_MYSQL_VERSION}/mariadb-java-client-${JDBC_MYSQL_VERSION}.jar

RUN curl -fSL https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.38.tar.gz -o /tmp/mysql.tgz
RUN mkdir /tmp/mysql
RUN tar -xvf /tmp/mysql.tgz -C /tmp/mysql --strip-components=1
RUN cp /tmp/mysql/*.jar /usr/local/lib/liquibase/lib

COPY liquibase.properties /tmp/liquibase.properties
COPY changelog.xml /tmp/changelog.xml
COPY migrate.sh /tmp/migrate.sh
RUN chmod 777 /tmp/migrate.sh

WORKDIR /tmp

ENTRYPOINT /tmp/migrate.sh
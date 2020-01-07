FROM alpine:latest

RUN apk add --update openjdk8-jre curl bash && rm -f /var/cache/apk/*

ENV LIQUIBASE_VERSION=3.6.3 \
    LIQUIBASE_PATH=/usr/local/lib/liquibase \
    LIQUIBASE_BIN=/usr/local/bin
    
ENV JDBC_POSTGRES_VERSION=42.2.5
ENV JDBC_POSTGRES_FILE_NAME=postgresql-${JDBC_POSTGRES_VERSION}.jar
ENV JDBC_POSTGRES_DOWNLOAD_URL=https://jdbc.postgresql.org/download/${JDBC_POSTGRES_FILE_NAME}

ENV JDBC_MYSQL_VERSION=8.0.15
ENV JDBC_MYSQL_FILE_NAME=mysql-connector-java-${JDBC_MYSQL_VERSION}.tar.gz
ENV JDBC_MYSQL_DOWNLOAD_URL=https://dev.mysql.com/get/Downloads/Connector-J/${JDBC_MYSQL_FILE_NAME}

RUN mkdir ${LIQUIBASE_PATH}
WORKDIR ${LIQUIBASE_PATH}
RUN curl -o /tmp/liquibase-${LIQUIBASE_VERSION}.tar.gz -sSL https://github.com/liquibase/liquibase/releases/download/liquibase-parent-${LIQUIBASE_VERSION}/liquibase-${LIQUIBASE_VERSION}-bin.tar.gz
RUN tar -zxf /tmp/liquibase-${LIQUIBASE_VERSION}.tar.gz -C ${LIQUIBASE_PATH}
RUN sed -i "s|bash$|ash|" ${LIQUIBASE_PATH}/liquibase
RUN chmod +x ${LIQUIBASE_PATH}/liquibase

RUN ln -s ${LIQUIBASE_PATH}/liquibase ${LIQUIBASE_BIN}

#Postgres driver
RUN curl -o ${LIQUIBASE_PATH}/lib/${JDBC_POSTGRES_FILE_NAME} ${JDBC_POSTGRES_DOWNLOAD_URL}

#MySql driver
RUN curl -fSL ${JDBC_MYSQL_DOWNLOAD_URL} -o /tmp/mysql.tgz
RUN mkdir /tmp/mysql && tar -xvf /tmp/mysql.tgz -C /tmp/mysql --strip-components=1
RUN cp /tmp/mysql/*.jar ${LIQUIBASE_PATH}/lib

COPY liquibase.properties /tmp/liquibase.properties
COPY changelog.xml /tmp/changelog.xml

RUN mkdir /tmp/changelogs

COPY update.sh /usr/local/bin/update.sh
RUN chmod 777 /usr/local/bin/update.sh

COPY diff.sh /usr/local/bin/diff.sh
RUN chmod 777 /usr/local/bin/diff.sh

COPY run.sh /usr/local/bin/run.sh
RUN chmod 777 /usr/local/bin/run.sh

WORKDIR /tmp

ENTRYPOINT [ "run.sh" ]
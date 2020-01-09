FROM progrium/busybox

ENV STAGE=development \
    TZ=CEST-2 \
    JAVA_HOME=/opt/jdk JAVA_VERSION_MAJOR=8 JAVA_VERSION_MINOR=131 JAVA_VERSION_BUILD=11 JAVA_PACKAGE=server-jre ORACLE_MF_STRING=d54c1d3a095b4ff2b6607d096fa80163\
    FLYWAY_HOME=/opt/flyway FLYWAY_VERSION=5.0.7 \
    GLASSFISH_HOME=/opt/glassfish GLASSFISH_VERSION=4.1 \
    H2_VERSION=1.4.191 DATABASE_DATA_DIR=/opt/data \
    GDRIVE_HOME=/opt/gdrive INSTANCE_NAME=default GDRIVE_TOKEN=/opt/gdrive/token \
    INSTALLATION_DIR=/install
    
ENV PATH=$PATH:${JAVA_HOME}/bin:${M2_HOME}/bin:${GLASSFISH_HOME}/bin:${GDRIVE_HOME}:${FLYWAY_HOME}

RUN opkg-install curl ca-certificates && rm -fr /tmp/* \
    && mkdir -p -m 775 ?/.gfclient \
    && curl -kLsSH "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-b${JAVA_VERSION_BUILD}/${ORACLE_MF_STRING}/${JAVA_PACKAGE}-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.tar.gz | gunzip -c - | tar -xf - -C /opt && mv /opt/jdk1.${JAVA_VERSION_MAJOR}.0_${JAVA_VERSION_MINOR} /opt/jdk \
    && curl -kLsS https://repo1.maven.org/maven2/org/flywaydb/flyway-commandline/${FLYWAY_VERSION}/flyway-commandline-${FLYWAY_VERSION}.tar.gz | gunzip -c | tar -xf - -C /opt && mv /opt/flyway-${FLYWAY_VERSION} ${FLYWAY_HOME} && rm -fr /tmp/* \
    && mkdir -p ${GLASSFISH_HOME} && wget -O "/tmp/glassfish.zip" "http://download.oracle.com/glassfish/${GLASSFISH_VERSION}/release/glassfish-${GLASSFISH_VERSION}.zip" && unzip /tmp/glassfish.zip -d /tmp/ && mv /tmp/glassfish?/* ${GLASSFISH_HOME} && chmod -R g+w ${GLASSFISH_HOME} && rm -fr /tmp/* \
    && mkdir -m 775 -p ${DATABASE_DATA_DIR} && wget -O ${GLASSFISH_HOME}/glassfish/domains/domain1/lib/ext/h2.jar http://repo2.maven.org/maven2/com/h2database/h2/${H2_VERSION}/h2-${H2_VERSION}.jar \
    && mkdir -m 775 -p ${GDRIVE_HOME} && curl -kLsSo "${GDRIVE_HOME}/gdrive" http://docs.google.com/uc?id=0B3X9GlR6EmbnQ0FtZmJJUXEyRTA && chmod -R +x ${GDRIVE_HOME} \
    && mkdir -m 775 -p ${INSTALLATION_DIR}

COPY resources/ /

RUN chmod -R 755 /scripts && chmod -R 775 /opt && chown -R 1001:root /opt

USER 1001

EXPOSE 8080 8181 4848 8082
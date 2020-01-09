FROM ubuntu:18.04
MAINTAINER Philipp Goellner, philipp.goellner@xaltbc.de

# setup useful environment variables
ENV BACKUP_HOST                                    false
ENV BACKUP_KEY_FILE                                /tmp/id_rsa
ENV BACKUP_PATH                                    false
ENV BACKUP_USER                                    false

ENV BAMBOO_VERSION                                 6.5.0
ENV BAMBOO_HOME                                    /var/atlassian/bamboo
ENV BAMBOO_INSTALL                                 /opt/atlassian/bamboo
ENV BAMBOO_REMOTE_DEBUG                            false
ENV BAMBOO_URL                                     https://www.atlassian.com/software/bamboo/downloads/binary/atlassian-bamboo-${BAMBOO_VERSION}.tar.gz

ENV DEBIAN_FRONTEND                                noninteractive

ENV DEBUG_PORT                                     5005
ENV HTTPS                                          false
ENV IMPORTCERT                                     false
ENV IMPORTPATH                                     /var/certificates
ENV PROXY_NAME                                     false
ENV RAM_MIN                                        1024
ENV RAM_MAX                                        2048

ENV LIQUIBASE                                      false
ENV LIQUIBASE_VERSION                              3.6.2
ENV LIQUIBASE_INSTALL                              /opt/liquibase
ENV LIQUIBASE_URL                                  https://github.com/liquibase/liquibase/releases/download/liquibase-parent-${LIQUIBASE_VERSION}/liquibase-${LIQUIBASE_VERSION}-bin.tar.gz

ENV MYSQL_DRIVER_VERSION                           5.1.36
ENV MYSQL_DRIVER_URL                               http://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-${MYSQL_DRIVER_VERSION}.tar.gz

ENV NEWRELIC_VERSION                               current
ENV NEWRELIC_APP_NAME                              bamboo-docker
ENV NEWRELIC_LICENSE                               false
ENV NEWRELIC_URL                                   https://download.newrelic.com/newrelic/java-agent/newrelic-agent/${NEWRELIC_VERSION}/newrelic-java.zip

ENV RUN_USER                                       daemon
ENV RUN_GROUP                                      daemon

ENV TIME_ZONE                                      false

ENV WAIT                                           false
ENV WAIT_COMMAND                                   none
ENV WAIT_SLEEP                                     2
ENV WAIT_LOOPS                                     10

# Install Java, git, other dependencies, download and extract Bamboo and create the required directory layout.
RUN apt-get update -qq \
 && apt-get install --no-install-recommends -qq -y gnupg2 \
                                                   lsb-release \
 && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys C2518248EEA14886 \
 && echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu/ $(lsb_release -s -c) main" > /etc/apt/sources.list.d/java.list \
 && echo "debconf shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections \
 && echo "debconf shared/accepted-oracle-license-v1-1 seen true"   | debconf-set-selections \
 && apt-get update -qq \
 && apt-get install --no-install-recommends -qq -y curl \
                                                   git \
                                                   openssh-client \
                                                   oracle-java8-installer \
                                                   rsync \
                                                   sed \
                                                   tzdata \
                                                   unzip \
                                                   xmlstarlet \
 && rm -rf                                         /var/lib/apt/lists/* \
 && mkdir -p                                       "${BAMBOO_INSTALL}" \
 && curl -Lsk                                      "${BAMBOO_URL}"       | tar -xz --directory "${BAMBOO_INSTALL}"     --strip-components=1 \
 && curl -Lsk                                      "${MYSQL_DRIVER_URL}" | tar -xz --directory "${BAMBOO_INSTALL}/lib" --strip-components=1 --no-same-owner "mysql-connector-java-${MYSQL_DRIVER_VERSION}/mysql-connector-java-${MYSQL_DRIVER_VERSION}-bin.jar" \
 && mkdir -p                                       "${LIQUIBASE_INSTALL}" \
 && curl -Lsk                                      "${LIQUIBASE_URL}"    | tar -xz --directory "${LIQUIBASE_INSTALL}" \
 && cp "${LIQUIBASE_INSTALL}/sdk/lib-sdk/slf4j-api-1.7.25.jar" "${LIQUIBASE_INSTALL}/lib/" \
 && curl -Lsk                                      "${NEWRELIC_URL}" -o                        /tmp/newrelic-java.zip \
 && unzip /tmp/newrelic-java.zip -d                "${BAMBOO_INSTALL}" \
 && rm -f /tmp/newrelic-java.zip \
 && mkdir                                          "${IMPORTPATH}" \
 && chown -R ${RUN_USER}:${RUN_GROUP}              "${IMPORTPATH}" \
                                                   "${BAMBOO_INSTALL}" \
                                                   /usr/lib/jvm/java-8-oracle/jre/lib/security/cacerts

COPY changelogs                                    "${LIQUIBASE_INSTALL}/changelogs/"
COPY liquibase.properties                          "${LIQUIBASE_INSTALL}/"
COPY configure-and-start-root.sh                   "${BAMBOO_INSTALL}/bin/"
COPY configure-and-start.sh                        "${BAMBOO_INSTALL}/bin/"
RUN chmod 500                                       ${BAMBOO_INSTALL}/bin/configure-and-start*.sh \
 && chown -R ${RUN_USER}:${RUN_GROUP}              "${BAMBOO_INSTALL}/bin/configure-and-start.sh" \
                                                   "${LIQUIBASE_INSTALL}"

# HTTP Port, Bamboo Agent Port
EXPOSE 8085 54663

VOLUME ["${BAMBOO_HOME}"]

WORKDIR ${BAMBOO_INSTALL}

# Run in foreground
ENTRYPOINT ["./bin/configure-and-start-root.sh"]

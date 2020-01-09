FROM sysreport/javabox
MAINTAINER Thoralf Liersch <thoralf.liersch@sysreport.de>

# Configuration variables.
ENV JIRA_VERSION_MAJOR=7 \
    JIRA_VERSION_MINOR=2 \
    JIRA_VERSION_BUILD=7 \
    JIRA_USER=jira

ENV JIRA_HOME=/var/atlassian/jira \
    JIRA_INSTALL=/opt/atlassian/jira \
    JIRA_VERSION=$JIRA_VERSION_MAJOR.$JIRA_VERSION_MINOR.$JIRA_VERSION_BUILD \
    JIRA_GROUP=${JIRA_USER}

RUN set -x \
    && apk add --no-cache \
        curl \
        tar \
        ca-certificates \
    && adduser -D -H ${JIRA_USER} \
    && mkdir -p                "${JIRA_HOME}" \
    && mkdir -p                "${JIRA_HOME}/caches/indexes" \
    && chmod -R 700            "${JIRA_HOME}" \
    && chown -R ${JIRA_USER}:${JIRA_GROUP}  "${JIRA_HOME}" \
    && mkdir -p                "${JIRA_INSTALL}/conf/Catalina" \
    && curl -Ls                "https://www.atlassian.com/software/jira/downloads/binary/atlassian-jira-software-${JIRA_VERSION}.tar.gz" | tar -xz --directory "${JIRA_INSTALL}" --strip-components=1 --no-same-owner \
    && curl -Ls                "https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.38.tar.gz" | tar -xz --directory "${JIRA_INSTALL}/lib" --strip-components=1 --no-same-owner "mysql-connector-java-5.1.38/mysql-connector-java-5.1.38-bin.jar" \
    && chmod -R 700            "${JIRA_INSTALL}/conf" \
    && chmod -R 700            "${JIRA_INSTALL}/logs" \
    && chmod -R 700            "${JIRA_INSTALL}/temp" \
    && chmod -R 700            "${JIRA_INSTALL}/work" \
    && chown -R ${JIRA_USER}:${JIRA_GROUP}  "${JIRA_INSTALL}/conf" \
    && chown -R ${JIRA_USER}:${JIRA_GROUP}  "${JIRA_INSTALL}/logs" \
    && chown -R ${JIRA_USER}:${JIRA_GROUP}  "${JIRA_INSTALL}/temp" \
    && chown -R ${JIRA_USER}:${JIRA_GROUP}  "${JIRA_INSTALL}/work" \
    && mkdir -p                "${JIRA_HOME}/data" \
    && mkdir -p                "${JIRA_HOME}/plugins" \
    && chown -R ${JIRA_USER}:${JIRA_GROUP} "${JIRA_HOME}/data" \
    && chown -R ${JIRA_USER}:${JIRA_GROUP} "${JIRA_HOME}/plugins" \
    && chmod -R 700            "${JIRA_HOME}/data" \
    && chmod -R 700            "${JIRA_HOME}/plugins" \
    && sed --in-place          "s/java version/openjdk version/g" "${JIRA_INSTALL}/bin/check-java.sh" \
    && echo -e                 "\njira.home=$JIRA_HOME" >> "${JIRA_INSTALL}/atlassian-jira/WEB-INF/classes/jira-application.properties" \
    && touch -d "@0"           "${JIRA_INSTALL}/conf/server.xml"


# Switch to the unprivileged user
USER ${JIRA_USER}:${JIRA_GROUP}

EXPOSE 8080
VOLUME ["/var/atlassian/jira", "/opt/atlassian/jira/logs"]
WORKDIR /var/atlassian/jira
COPY "script/startup.sh" "/"
COPY "mariadb-java-client-1.3.7.jar" "/opt/atlassian/jira/lib/"
COPY "dbconfig.xml" "/var/atlassian/jira/"
User root
RUN chmod +x /startup.sh
USER ${JIRA_USER}:${JIRA_GROUP}
ENTRYPOINT ["/startup.sh"]
CMD ["/opt/atlassian/jira/bin/catalina.sh", "run"]

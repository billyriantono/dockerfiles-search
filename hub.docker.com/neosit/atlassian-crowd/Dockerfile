FROM openjdk:8-alpine

# Configuration variables.
ENV CROWD_HOME     /var/atlassian/crowd
ENV CROWD_INSTALL  /opt/atlassian/crowd
ENV CROWD_VERSION  3.4.3
ENV POSTGRES_JDBC_VERSION 42.2.5
ENV MYSQL_JDBC_VERSION 8.0.13

# Install Atlassian Crowd and helper tools and setup initial home
# directory structure.
RUN set -x \
    && apk add --no-cache curl xmlstarlet bash ttf-dejavu libc6-compat \
    && mkdir -p                "${CROWD_HOME}" \
    && chmod -R 700            "${CROWD_HOME}" \
    && chown -R daemon:daemon  "${CROWD_HOME}" \
    && mkdir -p                "${CROWD_INSTALL}/apache-tomcat/conf/Catalina" \
    && curl -Ls                "https://www.atlassian.com/software/crowd/downloads/binary/atlassian-crowd-${CROWD_VERSION}.tar.gz" | tar -xz --directory "${CROWD_INSTALL}" --strip-components=1 --no-same-owner \
    && rm -f                   "${CROWD_INSTALL}/apache-tomcat/lib/mysql-connector*.jar" \
    && rm -f                   "${CROWD_INSTALL}/apache-tomcat/lib/postgresql-*.jar" \
    && curl -Ls                "https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-${MYSQL_JDBC_VERSION}.tar.gz" | tar -xz --directory "${CROWD_INSTALL}/apache-tomcat/lib" --strip-components=1 --no-same-owner "mysql-connector-java-${MYSQL_JDBC_VERSION}/mysql-connector-java-${MYSQL_JDBC_VERSION}.jar" \
    && curl -Ls                "https://jdbc.postgresql.org/download/postgresql-${POSTGRES_JDBC_VERSION}.jar" -o "${CROWD_INSTALL}/apache-tomcat/lib/postgresql-${POSTGRES_JDBC_VERSION}.jar" \
    && chmod -R 700            "${CROWD_INSTALL}/apache-tomcat/conf" \
    && chmod -R 700            "${CROWD_INSTALL}/apache-tomcat/logs" \
    && chmod -R 700            "${CROWD_INSTALL}/apache-tomcat/temp" \
    && chmod -R 700            "${CROWD_INSTALL}/apache-tomcat/work" \
    && chown -R daemon:daemon  "${CROWD_INSTALL}/apache-tomcat/conf" \
    && chown -R daemon:daemon  "${CROWD_INSTALL}/apache-tomcat/logs" \
    && chown -R daemon:daemon  "${CROWD_INSTALL}/apache-tomcat/temp" \
    && chown -R daemon:daemon  "${CROWD_INSTALL}/apache-tomcat/work" \
    && echo -e                 "\ncrowd.home=$CROWD_HOME" >> "${CROWD_INSTALL}/crowd-webapp/WEB-INF/classes/crowd-init.properties" \
    && touch -d "@0"           "${CROWD_INSTALL}/apache-tomcat/conf/server.xml" \
    && chmod 777               "${CROWD_INSTALL}/start_crowd.sh" \
    && chmod 777               "${CROWD_INSTALL}/stop_crowd.sh" \
    && chmod 777               "${CROWD_INSTALL}/apache-tomcat/bin/catalina.sh" \
    && rm -rf                  "${CROWD_INSTALL}/crowd-openidclient-webapp" \
    && rm -rf                  "${CROWD_INSTALL}/crowd-openidserver-webapp" \
    && rm -rf                  "${CROWD_INSTALL}/apache-tomcat/conf/Catalina/localhost/openidclient.xml" \
    && rm -rf                  "${CROWD_INSTALL}/apache-tomcat/conf/Catalina/localhost/openidserver.xml"

# Use the default unprivileged account. This could be considered bad practice
# on systems where multiple processes end up being executed by 'daemon' but
# here we only ever run one process anyway.
USER daemon:daemon

# Expose default HTTP connector port.
EXPOSE 8095

# Set volume mount points for installation and home directory. Changes to the
# home directory needs to be persisted as well as parts of the installation
# directory due to eg. logs.
VOLUME ["/var/atlassian/crowd", "/opt/atlassian/crowd/apache-tomcat/logs"]

# Set the default working directory as the installation directory.
WORKDIR /var/atlassian/crowd

COPY "docker-entrypoint.sh" "/"
ENTRYPOINT ["/docker-entrypoint.sh"]

# Run Atlassian Crowd as a foreground process by default.
CMD ["/opt/atlassian/crowd/start_crowd.sh", "-fg"]

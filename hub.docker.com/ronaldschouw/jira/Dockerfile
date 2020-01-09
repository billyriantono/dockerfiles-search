FROM anapsix/alpine-java:jdk

#  Setup useful environment variables
#
ENV JIRA_HOME     /var/atlassian/jira
ENV JIRA_INSTALL  /opt/atlassian/jira
ENV JIRA_VERSION  7.5.0

# Install Atlassian Confluence and hepler tools and setup initial home
# directory structure.


RUN apk add --no-cache --update curl tar tzdata \
    && cp /usr/share/zoneinfo/Europe/Amsterdam /etc/localtime  \
    && mkdir -p                "${JIRA_HOME}" \
    && mkdir -p                "${JIRA_INSTALL}"\
    && curl -Ls                "https://www.atlassian.com/software/jira/downloads/binary/atlassian-jira-software-${JIRA_VERSION}.tar.gz"  | tar -xz --directory "${JIRA_INSTALL}" --strip-components=1 --no-same-owner \
    && echo -e                 "\njira.home=$JIRA_HOME" > "${JIRA_INSTALL}/atlassian-jira/WEB-INF/classes/jira-application.properties" \
    && chown -R daemon:daemon  "${JIRA_INSTALL}"


#ADD server.xml ${JIRA_INSTALL}/conf/server.xml
ADD setenv.sh ${JIRA_INSTALL}/bin/setenv.sh
#RUN chown daemon:daemon ${JIRA_INSTALL}/conf/server.xml
RUN chown daemon:daemon ${JIRA_INSTALL}/bin/setenv.sh

# Use the default unprivileged account. This could be considered bad practice
# on systems where multiple processes end up being executed by 'daemin' but
# here we only ever run one process anyway.
USER daemon:daemon

# Expose default HTTP connector port.
EXPOSE 8080

# Set volume mount points for installation and home directory. Changes to the
# home directory needs to be persisted as well as parts of the installation
# directory due to eg. logs.

VOLUME ${JIRA_HOME}


# Set the default working directory as the Confluence home directory.
WORKDIR ${JIRA_INSTALL}

# Run Atlassian Confluence as a foreground process by default.
#
CMD ["./bin/catalina.sh", "run"]

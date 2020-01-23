FROM ubuntu:14.04
MAINTAINER boris.georgiev@botronsoft.com

# Configuration variables.
ENV JIRA_HOME     /var/atlassian/jira
ENV JIRA_INSTALL  /opt/atlassian/jira
ENV JIRA_VERSION  6.4.12

RUN set -x \
    && apt-get update --quiet \
    && apt-get install --quiet --yes --no-install-recommends \
    libtcnative-1 xmlstarlet curl \
    && apt-get clean

# Download and install JIRA
COPY response.varfile /tmp/
RUN set -x \
    && sed --in-place "s@sys.installationDir=@sys.installationDir=${JIRA_INSTALL}@g" "/tmp/response.varfile" \
    && sed --in-place "s@app.jiraHome=@app.jiraHome=${JIRA_HOME}@g" "/tmp/response.varfile" \
    && curl -LOk https://www.atlassian.com/software/jira/downloads/binary/atlassian-jira-${JIRA_VERSION}-x64.bin \
    && chmod +x atlassian-jira-${JIRA_VERSION}-x64.bin \
    && /bin/bash atlassian-jira-${JIRA_VERSION}-x64.bin -q -varfile /tmp/response.varfile \
    && rm atlassian-jira-${JIRA_VERSION}-x64.bin

# Install SmartCom certificates
COPY installsmartcomcerts.sh /tmp/
RUN set -x \
    && sed --in-place "s@JAVA_HOME=@JAVA_HOME=${JIRA_INSTALL}@g" "/tmp/installsmartcomcerts.sh" \
    && chmod +x /tmp/installsmartcomcerts.sh \
    && /bin/bash /tmp/installsmartcomcerts.sh    

# Expose default HTTP connector port.
EXPOSE 8080

# Set volume mount points for installation and home directory. Changes to the
# home directory needs to be persisted as well as parts of the installation
# directory due to eg. logs.
VOLUME ["/var/atlassian/jira"]

# Set the default working directory as the installation directory.
WORKDIR ${JIRA_HOME}

# Run JIRA as a service
CMD $JIRA_INSTALL/bin/start-jira.sh -fg

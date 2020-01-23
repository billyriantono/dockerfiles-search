# JIRA
FROM ubuntu:18.04

##############
# Setup JIRA #
##############
ENV JIRA_VERSION=8.4.0

RUN apt-get update && apt-get install -y wget xmlstarlet fontconfig
#COPY atlassian-jira-software-${JIRA_VERSION}-x64.bin /opt
WORKDIR /opt
RUN wget https://www.atlassian.com/software/jira/downloads/binary/atlassian-jira-software-${JIRA_VERSION}-x64.bin
COPY jira-unhattended.varfile /tmp/response.varfile
RUN chmod a+x atlassian-jira-software-${JIRA_VERSION}-x64.bin
RUN ./atlassian-jira-software-${JIRA_VERSION}-x64.bin -q -varfile /tmp/response.varfile


# Copy and symlink the config folder to make it persistent
WORKDIR /opt/atlassian/jira
RUN mv conf /var/atlassian/application-data/jira && ln -s /var/atlassian/application-data/jira/conf conf

VOLUME ["/var/atlassian/application-data/jira", "/opt/atlassian/jira"]



EXPOSE 8080
COPY ./docker-entrypoint.sh /
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["start-jira"]

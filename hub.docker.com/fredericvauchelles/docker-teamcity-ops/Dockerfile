FROM postgres:9.5

# Setup useful environment variables
ENV CONF_HOME             /var/atlassian/teamcity
ENV CONF_INSTALL          /opt/atlassian/teamcity

COPY docker-entrypoint.sh /
RUN  chmod 755 /docker-entrypoint.sh

WORKDIR ${CONF_HOME}

ENTRYPOINT ["/docker-entrypoint.sh"]
ARG WILDFLY_VERSION

FROM jboss/wildfly:${WILDFLY_VERSION:-17.0.0.Final}

ARG ADMIN_USER
ARG ADMIN_SECRET
ARG SCRIPT_DIR

ENV ADMIN_USER=${ADMIN_USER:-admin} \
    ADMIN_SECRET=${ADMIN_SECRET:-Admin#70365} \
    SCRIPT_DIR=${SCRIPT_DIR:-/opt/scripts}

USER root

COPY ./docker-entrypoint.sh /opt/jboss/wildfly/bin/docker-entrypoint.sh

RUN yum install -y dos2unix && yum clean all && rm -rf /var/cache/yum \
  && \
    chown jboss:jboss /opt/jboss/wildfly/bin/docker-entrypoint.sh && \
    chmod +x /opt/jboss/wildfly/bin/docker-entrypoint.sh \
  && \
    mkdir -p ${SCRIPT_DIR} && \
    chown jboss:jboss ${SCRIPT_DIR}

USER jboss

ENTRYPOINT ["/opt/jboss/wildfly/bin/docker-entrypoint.sh"]

# Boot in standalone mode (default)
CMD ["/opt/jboss/wildfly/bin/standalone.sh","-b","0.0.0.0","-bmanagement","0.0.0.0"]

# Boot in domain-mode:
#CMD ["/opt/jboss/wildfly/bin/domain.sh","-b","0.0.0.0","-bmanagement","0.0.0.0"]

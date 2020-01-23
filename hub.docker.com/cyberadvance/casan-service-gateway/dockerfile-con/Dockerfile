FROM jenkins/jenkins:2.190.2-alpine

USER root
ENV JAVA_OPTS -Djenkins.install.runSetupWizard=false
RUN /usr/local/bin/install-plugins.sh git build-timeout credentials-binding \
                                      timestamper ws-cleanup ssh-slaves \
                                      workflow-aggregator pipeline-stage-view

COPY docker-entrypoint.sh /usr/local/bin
RUN chmod +x /usr/local/bin/docker-entrypoint.sh

USER jenkins

VOLUME ["/var/lib/containers/storage"]

ENTRYPOINT ["/sbin/tini", "--", "docker-entrypoint.sh"]
CMD ["/usr/local/bin/jenkins.sh"]
FROM jenkins/jenkins:2.206-alpine
USER root

# Install some basic dependencies
RUN apk --no-cache add \
	bash \
	curl \
	git \
	make \
	su-exec

COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt
RUN echo 2.0 > /usr/share/jenkins/ref/jenkins.install.UpgradeWizard.state

ENV JENKINS_MEMORY=512M
ENV MYTIMEZONE=America/Los_Angeles
ENV JENKINS_EXECUTORS=3
ENV JENKINS_ADMIN_USR=admin
ENV JENKINS_ADMIN_PSW=password
ENV JENKINS_WORKSPACE_MAX_AGE=3
ENV JENKINS_URL=http://localhost:8080

# Invert these flags if you want to keep the plugins from the local installation instead.
ENV TRY_UPGRADE_IF_NO_MARKER=true
ENV PLUGINS_FORCE_UPGRADE=true

COPY docker-entrypoint.sh /
COPY init.groovy.d/* /usr/share/jenkins/ref/init.groovy.d/

RUN mkdir -p /var/jenkins_home
WORKDIR /var/jenkins_home
VOLUME ["/var/jenkins_home"]

ENTRYPOINT ["/sbin/tini", "-g", "--", "/docker-entrypoint.sh"]
CMD ["server"]

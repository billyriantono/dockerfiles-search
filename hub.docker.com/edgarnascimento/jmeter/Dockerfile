# inspired by https://github.com/hauptmedia/docker-jmeter  and
# https://github.com/hhcordero/docker-jmeter-server/blob/master/Dockerfile
FROM alpine:3.9

ARG JMETER_VERSION="5.1.1"
ENV JMETER_HOME /opt/apache-jmeter-${JMETER_VERSION}
ENV	JMETER_BIN	${JMETER_HOME}/bin
ENV	JMETER_DOWNLOAD_URL  https://archive.apache.org/dist/jmeter/binaries/apache-jmeter-${JMETER_VERSION}.tgz
ARG PLUGINS_MANAGER_VERSION="1.3"
ENV PLUGINS_MANAGER_URL http://search.maven.org/remotecontent?filepath=kg/apc/jmeter-plugins-manager/${PLUGINS_MANAGER_VERSION}/jmeter-plugins-manager-${PLUGINS_MANAGER_VERSION}.jar
ARG COMMAND_RUNNER_VERSION="2.2"
ENV COMMAND_RUNNER_URL http://search.maven.org/remotecontent?filepath=kg/apc/cmdrunner/${COMMAND_RUNNER_VERSION}/cmdrunner-${COMMAND_RUNNER_VERSION}.jar 

# Install extra packages
# See https://github.com/gliderlabs/docker-alpine/issues/136#issuecomment-272703023
RUN    apk update \
	&& apk upgrade \
	&& apk add ca-certificates \
	&& update-ca-certificates \
	&& apk add --update openjdk8-jre tzdata curl unzip bash \
	&& apk add --no-cache nss \
	&& rm -rf /var/cache/apk/* \
	&& mkdir -p /tmp/dependencies  \
	&& curl -L --silent ${JMETER_DOWNLOAD_URL} >  /tmp/dependencies/apache-jmeter-${JMETER_VERSION}.tgz  \
	&& mkdir -p /opt  \
	&& tar -xzf /tmp/dependencies/apache-jmeter-${JMETER_VERSION}.tgz -C /opt  \
	&& rm -rf /tmp/dependencies

# Install Plugins Manager and Command Runner
RUN	curl -L --silent ${PLUGINS_MANAGER_URL} > ${JMETER_HOME}/lib/ext/jmeter-plugins-manager-${PLUGINS_MANAGER_VERSION}.jar \
	&& curl -L --silent ${COMMAND_RUNNER_URL} > ${JMETER_HOME}/lib/cmdrunner-${COMMAND_RUNNER_VERSION}.jar \
	&& java -cp ${JMETER_HOME}/lib/ext/jmeter-plugins-manager-${PLUGINS_MANAGER_VERSION}.jar org.jmeterplugins.repository.PluginManagerCMDInstaller \
	&& ${JMETER_HOME}/bin/PluginsManagerCMD.sh install jpgc-casutg

# TODO: plugins (later)
# && unzip -oq "/tmp/dependencies/JMeterPlugins-*.zip" -d $JMETER_HOME

# Change TimeZone
ENV TZ="America/Sao_Paulo"

# Set global PATH such that "jmeter" command is found
ENV PATH $PATH:$JMETER_BIN

# Entrypoint has same signature as "jmeter" command
COPY entrypoint.sh /

WORKDIR	${JMETER_HOME}

ENTRYPOINT ["/entrypoint.sh"]
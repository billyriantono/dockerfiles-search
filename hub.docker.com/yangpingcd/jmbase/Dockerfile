FROM alpine:3.8

LABEL maintainer="Ping Yang<ping@sliq.com>"

ARG JMETER_VERSION="5.0"
ENV JMETER_HOME /opt/apache-jmeter-${JMETER_VERSION}
ENV	JMETER_BIN	${JMETER_HOME}/bin
ENV	JMETER_DOWNLOAD_URL https://archive.apache.org/dist/jmeter/binaries/apache-jmeter-${JMETER_VERSION}.tgz

# Install extra packages
# See https://github.com/gliderlabs/docker-alpine/issues/136#issuecomment-272703023
# Change TimeZone TODO: TZ still is not set!
ARG TZ="Europe/Amsterdam"
RUN apk update \
&& apk upgrade \
&& apk add ca-certificates \
&& update-ca-certificates \
&& apk add --update openjdk8-jre tzdata curl unzip bash \
&& rm -rf /var/cache/apk/* \
&& mkdir -p /tmp/dependencies \
&& curl -L --silent ${JMETER_DOWNLOAD_URL} > /tmp/dependencies/apache-jmeter-${JMETER_VERSION}.tgz \
&& mkdir -p /opt \
&& tar -xzf /tmp/dependencies/apache-jmeter-${JMETER_VERSION}.tgz -C /opt \
&& rm -rf /tmp/dependencies

# TODO: plugins (later)
# && unzip -oq "/tmp/dependencies/JMeterPlugins-*.zip" -d $JMETER_HOME

# Set global PATH such that "jmeter" command is found
ENV PATH $PATH:$JMETER_BIN


WORKDIR	${JMETER_HOME}

CMD ["bash"]

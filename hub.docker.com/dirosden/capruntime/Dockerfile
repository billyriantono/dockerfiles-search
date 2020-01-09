FROM gliderlabs/alpine

LABEL name="Alpine OS Base Image"
LABEL vendor="AlpineOS"
LABEL license=GPLv2

ENV REFRESHED_AT 2017-APR-10
ENV GLIBC_VERSION="2.23-r2"

RUN apk update && \
    apk add bash curl

RUN apk upgrade --update && \
    apk add curl sed && \
    apk --update add tar && \
    for pkg in glibc glibc-bin glibc-i18n; do curl -sSL https://github.com/sgerrand/alpine-pkg-glibc/releases/download/$GLIBC_VERSION/${pkg}-$GLIBC_VERSION.apk -o /tmp/${pkg}-$GLIBC_VERSION.apk; done && \
    apk add --allow-untrusted /tmp/glibc-*.apk && \
    rm -v /tmp/*.apk && \
    ( /usr/glibc-compat/bin/localedef --force --inputfile POSIX --charmap UTF-8 C.UTF-8 || true ) && \
    echo "export LANG=C.UTF-8" > /etc/profile.d/locale.sh && \
    /usr/glibc-compat/sbin/ldconfig /lib /usr/glibc-compat/lib && \
    echo 'hosts: files mdns4_minimal [NOTFOUND=return] dns mdns4' >> /etc/nsswitch.conf
        
RUN { \
		echo '#!/bin/sh'; \
		echo 'set -e'; \
		echo; \
		echo 'dirname "$(dirname "$(readlink -f "$(which javac || which java)")")"'; \
	} > /usr/local/bin/docker-java-home \
	&& chmod +x /usr/local/bin/docker-java-home
ENV JAVA_HOME /usr/lib/jvm/java-1.8-openjdk/jre
ENV PATH $PATH:/usr/lib/jvm/java-1.8-openjdk/jre/bin:/usr/lib/jvm/java-1.8-openjdk/bin

ENV JAVA_VERSION 8u92
ENV JAVA_ALPINE_VERSION 8.111.14-r0

RUN set -x \
	&& apk add --no-cache \
		openjdk8-jre="$JAVA_ALPINE_VERSION" \
&& [ "$JAVA_HOME" = "$(docker-java-home)" ]


# - Install basic packages (e.g. python-setuptools is required to have python's easy_install)
# - Install yum-utils so we have yum-config-manager tool available
# - Install inotify, needed to automate daemon restarts after config file changes
# - Install jq, small library for handling JSON files/api from CLI
# - Install supervisord (via python's easy_install - as it has the newest 3.x version)

RUN echo "http://dl-cdn.alpinelinux.org/alpine/v3.4/community" >> /etc/apk/repositories && \
    echo "http://dl-cdn.alpinelinux.org/alpine/v3.4/main" >> /etc/apk/repositories      && \
    echo "http://alpine.gliderlabs.com/alpine/edge/community" >> /etc/apk/repositories  && \
    echo "http://alpine.gliderlabs.com/alpine/edge/testing" >> /etc/apk/repositories    && \
    echo "http://alpine.gliderlabs.com/alpine/edge/main" >> /etc/apk/repositories


# Salt and prerequisites
RUN apk update && \
    apk add unzip iproute2 py-setuptools which jq supervisor
    
RUN apk add salt-minion py-inotify

ENV MULE_HOME /opt/mule
ENV MULE_VERSION 3.8.0

# -- START - REPLACE WITH NEXUS REPO AUTH CRED IF YOU HAVE A ENTERPRISE LICENSE --

# RUN set -x \
#          && mkdir /opt \
#         && cd /opt \
#         && curl -o mule.zip -H "Authorization: Basic XXXXXXXXX" https://repository.mulesoft.org/nexus/content/repositories/releases-ee/com/mulesoft/muleesb/distributions/mule-ee-distribution-standalone/$MULE_VERSION/mule-ee-distribution-standalone-$MULE_VERSION.zip \
#         && unzip mule.zip \
#         && mv mule-enterprise-standalone-$MULE_VERSION mule \
#         && rm mule.zip* \
#         && find . -name "*freebsd*.*" -type f -delete \
#         && find . -name "*aix*.*" -type f -delete \
#         && find . -name "*hpux*.*" -type f -delete \
#         && find . -name "*solaris*.*" -type f -delete \
#         && find . -name "*macosx*.*" -type f -delete \
#         && find . -name "*windows*.*" -type f -delete 

RUN set -x \
        && mkdir /opt \
        && cd /opt \
        && curl -o mule.zip https://repository-master.mulesoft.org/nexus/content/repositories/releases/org/mule/distributions/mule-standalone/$MULE_VERSION/mule-standalone-$MULE_VERSION.zip \
        && unzip mule.zip \
        && mv mule-standalone-$MULE_VERSION mule \
        && rm mule.zip* \
        && find . -name "*freebsd*.*" -type f -delete \
        && find . -name "*aix*.*" -type f -delete \
        && find . -name "*hpux*.*" -type f -delete \
        && find . -name "*solaris*.*" -type f -delete \
        && find . -name "*macosx*.*" -type f -delete \
        && find . -name "*windows*.*" -type f -delete 
        
# -- START - UNCOMMENT THIS IF YOU HAVE A ENTERPRISE LICENSE --

## Move Enterprise License Key for Mule 
#COPY srv/mule/muleLicenseKey.lic /opt/mule/license/license.lic

# -- END - UNCOMMENT THIS IF YOU HAVE A ENTERPRISE LICENSE --

# - Get Prometheus JMX Exporter

RUN set -x \
        && curl -o jmx_prom.jar http://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_javaagent/0.9/jmx_prometheus_javaagent-0.9.jar \
        && mkdir /opt/mule/lib/agent  \
        && mv jmx_prom.jar /opt/mule/lib/agent/jmx_prom.jar

# Moving Runtime Configuration for Main Components - Supervisor and Salt Minion 
ADD etc	     /etc 
ADD config   /config

RUN mkdir -p /var/log/supervisor

# Expose volumes
VOLUME ["/var/log/supervisor"]

# Exposing Proxy ports
EXPOSE 8081
EXPOSE 1099
EXPOSE 1199

RUN ["chmod", "+x", "/config/bootstrap.sh"]
RUN ["chmod", "+x", "/config/init/configureenv.sh"]
RUN ["chmod", "+x", "/config/init/setupminion.sh"]

#Running the Start Script
CMD ["/config/bootstrap.sh"]



FROM redis:5.0

MAINTAINER tomas.hejatko@ackee.cz

COPY ackee-entrypoint.sh /ackee-entrypoint.sh

RUN apt-get -qq update
RUN DEBIAN_FRONTEND=noninteractive apt-get -y -q install curl gnupg ca-certificates lsb-release libhiredis0.13 procps
RUN DEBIAN_FRONTEND=noninteractive apt-get -y upgrade

# Stackdriver

RUN echo "deb http://packages.cloud.google.com/apt google-cloud-monitoring-$(lsb_release -sc) main" > /etc/apt/sources.list.d/google-cloud-monitoring.list
RUN curl --connect-timeout 5 -s -f "https://packages.cloud.google.com/apt/doc/apt-key.gpg" | apt-key add -
RUN apt-get -qq update
RUN DEBIAN_FRONTEND=noninteractive apt-get -y -q install stackdriver-agent

RUN rm -rf /var/lib/apt/lists/*

#COPY setup_stackdriver.sh /opt/01-setup-stackdriver.sh

RUN cp /usr/local/bin/docker-entrypoint.sh /opt/04-redis-entrypoint.sh && cp /ackee-entrypoint.sh /usr/local/bin/docker-entrypoint.sh

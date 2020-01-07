# PixelHyperlink Ubuntu with Monitoring tools Docker
#
# VERSION               1.0.0

FROM pixelhyperlinkdockers/ubuntu:v1.8.0
MAINTAINER Abhishek Salian <abhi@pixelhyperlink.com>

LABEL Description="This image contains base ubuntu os with monitoring tools."
LABEL Vendor="PixelHyperlink"
LABEL Version="1.0.0"
LABEL com.pixelhyperlink.docker.ubuntumon.version="1.0.0"
LABEL vendor="PixelHyperlink"
LABEL com.pixelhyperlink.docker.ubuntumon.release-date="2017-07-14"
LABEL com.pixelhyperlink.docker.ubuntumon.version.is-production="true"

ENV REQUIRES_SETUP 1

EXPOSE 4949

RUN wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | \
	apt-key add - && \
	apt-get -y install apt-transport-https && \
	echo "deb https://artifacts.elastic.co/packages/5.x/apt stable main" | \
	tee -a /etc/apt/sources.list.d/elastic-5.x.list && \
	apt-get update && \
	apt-get install -y netcat \
		metricbeat \
		packetbeat \
		munin-node

RUN mkdir /var/log/heartbeat /var/lib/heartbeat /var/lib/metricbeat /var/log/metricbeat /var/lib/packetbeat /var/log/packetbeat /var/run/munin

VOLUME ["/var/log/heartbeat", "/var/lib/heartbeat", "/var/lib/metricbeat", "/var/log/metricbeat", "/var/lib/packetbeat", "/var/log/packetbeat", "/var/log/munin"]

# Copy heartbeat setup.
COPY ./heartbeat /opt/heartbeat

# Install heartbeat
RUN dpkg -i /opt/heartbeat/heartbeat-5.5.0-amd64.deb

# Copy metricbeat config.
COPY ./metricbeat.yml /etc/metricbeat/metricbeat.yml

# Copy heartbeat config.
COPY ./heartbeat.yml /etc/heartbeat/heartbeat.yml

# Copy packetbeat config.
COPY ./packetbeat.yml /etc/packetbeat/packetbeat.yml

COPY ./monitoring_entrypoint.sh /opt/monitoring_entrypoint.sh

# Copy munin node config
COPY ./munin-node.conf /etc/munin/munin-node.conf

# Run startup scripts
RUN chmod 777 /opt/monitoring_entrypoint.sh

ENTRYPOINT ["/opt/monitoring_entrypoint.sh"]
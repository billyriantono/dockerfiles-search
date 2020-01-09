# PixelHyperlink Ubuntu with Beat Docker
#
# VERSION               1.0.0

FROM pixelhyperlinkdockers/ubuntu:v1.8.0
MAINTAINER Abhishek Salian <abhi@pixelhyperlink.com>

LABEL Description="This image contains base ubuntu os with metricbeat service."
LABEL Vendor="PixelHyperlink"
LABEL Version="1.0.0"
LABEL com.pixelhyperlink.docker.beats.version="1.0.0"
LABEL vendor="PixelHyperlink"
LABEL com.pixelhyperlink.docker.metricbeat.release-date="2017-07-06"
LABEL com.pixelhyperlink.docker.metricbeat.version.is-production="true"

RUN wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | \
	apt-key add - && \
	apt-get -y install apt-transport-https && \
	echo "deb https://artifacts.elastic.co/packages/5.x/apt stable main" | \
	tee -a /etc/apt/sources.list.d/elastic-5.x.list && \
	apt-get update && \
	apt-get install -y metricbeat

RUN mkdir /var/lib/metricbeat /var/log/metricbeat

VOLUME ["/var/lib/metricbeat", "/var/log/metricbeat"]

# Copy metricbeat config.
COPY ./metricbeat.yml /etc/metricbeat/metricbeat.yml

COPY ./metricbeat_entrypoint.sh /opt/metricbeat_entrypoint.sh

# Run startup scripts
RUN chmod 777 /opt/metricbeat_entrypoint.sh

ENTRYPOINT ["/opt/metricbeat_entrypoint.sh"]

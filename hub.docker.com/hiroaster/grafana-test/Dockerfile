FROM ubuntu
MAINTAINER Wenyang <fengwenyang@gmail.com>
# Install Grafana
ENV GRAFANA_VERSION 2.6.0
RUN apt-get -y  install libfontconfig curl ca-certificates
COPY grafana_${GRAFANA_VERSION}_amd64.deb  /tmp/grafana_${GRAFANA_VERSION}_amd64.deb
COPY run.sh /tmp/run.sh
RUN dpkg -i /tmp/grafana_${GRAFANA_VERSION}_amd64.deb

VOLUME ["/var/lib/grafana", "/var/log/grafana", "/etc/grafana"]

EXPOSE 3000


ENTRYPOINT ["/tmp/run.sh"]

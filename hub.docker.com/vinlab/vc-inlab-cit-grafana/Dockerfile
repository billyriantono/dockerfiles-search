FROM grafana/grafana:6.0.0-beta3
ADD ./provisioning /etc/grafana/provisioning
ADD ./grafana-config.ini /etc/grafana/grafana-config.ini

# Provision plugins
ADD ./plugins /etc/grafana/plugins

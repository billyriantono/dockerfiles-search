FROM grafana/grafana:5.2.2

COPY provisioning/datasources/datasource.yaml /etc/grafana/provisioning/datasources/datasource.yaml
COPY provisioning/dashboards/dashboard.yaml /etc/grafana/provisioning/dashboards/dashboard.yaml
ADD dashboards /var/lib/grafana/dashboards/
ENV GF_PATHS_PROVISIONING=/etc/grafana/provisioning


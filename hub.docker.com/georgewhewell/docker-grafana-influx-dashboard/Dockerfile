FROM grafana/grafana

COPY grafana-influx-dashboard grafana-influx-dashboard
WORKDIR grafana-influx-dashboard
RUN ./install.sh /usr/share/grafana

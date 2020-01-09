FROM grafana/grafana:latest

USER root
RUN apt-get update && apt-get install -y curl gettext-base && rm -rf /var/lib/apt/lists/*
USER grafana
WORKDIR /etc/grafana

WORKDIR /app
COPY entrypoint.sh ./

USER root
RUN chmod u+x entrypoint.sh

USER grafana
VOLUME ["/etc/grafana/datasources", "/etc/grafana/dashboards"]
EXPOSE 3000

ENTRYPOINT ["/app/entrypoint.sh"]
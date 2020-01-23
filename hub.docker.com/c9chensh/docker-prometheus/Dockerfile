FROM prom/prometheus:v2.1.0

COPY conf /etc/prometheus/
COPY rules/alert.rules /etc/prometheus/alert.rules

ENTRYPOINT [ "/etc/prometheus/docker-entrypoint.sh" ]
CMD        [ "-config.file=/etc/prometheus/prometheus.yml", \
             "-storage.local.path=/prometheus", \
             "-web.console.libraries=/etc/prometheus/console_libraries", \
             "-web.console.templates=/etc/prometheus/consoles" ]
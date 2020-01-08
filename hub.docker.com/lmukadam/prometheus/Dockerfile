FROM        prom/prometheus
ADD         ./prometheus.yml  /etc/prometheus/prometheus.yml
EXPOSE      9090
ENTRYPOINT  [ "/bin/prometheus" ]
CMD         [ "-config.file=/etc/prometheus/prometheus.yml", \
              "-storage.local.path=/prometheus", \
              "-web.console.libraries=/etc/prometheus/console_libraries", \
              "-web.console.templates=/etc/prometheus/consoles" ]
FROM braedon/prometheus-kafka-consumer-group-exporter:0.2.0

ENV DNS_DOMAIN=""
ENTRYPOINT /usr/local/bin/prometheus-kafka-consumer-group-exporter -b kafka-bootstrap01.${DNS_DOMAIN}

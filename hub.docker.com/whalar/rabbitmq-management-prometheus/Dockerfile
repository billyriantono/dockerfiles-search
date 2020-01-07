FROM rabbitmq:3-management
COPY install_prometheus_exporter.sh /
RUN apt-get update && apt-get install curl -y && sh install_prometheus_exporter.sh

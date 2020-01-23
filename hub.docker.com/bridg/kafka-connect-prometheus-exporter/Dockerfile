FROM python:3.6.2-slim

RUN pip install prometheus_client

ENV KAFKA_CONNECT_URL ""
ENV KAFKA_CONNECT_PORT 8083
ENV METRICS_PORT 9118
COPY kafka_connect_status_prometheus_exporter.py /usr/local/bin/

CMD python /usr/local/bin/kafka_connect_status_prometheus_exporter.py ${KAFKA_CONNECT_URL} ${KAFKA_CONNECT_PORT} ${METRICS_PORT}

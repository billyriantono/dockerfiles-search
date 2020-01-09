FROM python:3.7-slim

ENV MQTT_HOST=192.168.1.2
ENV MQTT_PORT=1883
ENV MQTT_USER=mqtt
ENV MQTT_PASS=mqtt
ENV TTY_PATH=/dev/ttyACM0

ENTRYPOINT ["python3.7", "/opt/exporter/main.py"]
COPY exporter /opt/exporter
WORKDIR /opt/exporter
RUN pip install -r requirements.txt

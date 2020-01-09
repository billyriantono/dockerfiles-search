FROM python:3.7-alpine

EXPOSE 9180
ENTRYPOINT ["/opt/exporter/run.py", "--host=0.0.0.0"]

COPY run.py /opt/exporter/run.py
COPY setup.py /opt/exporter/setup.py
COPY iot_exporter  /opt/exporter/iot_exporter

RUN chmod +x /opt/exporter/run.py && pip install /opt/exporter

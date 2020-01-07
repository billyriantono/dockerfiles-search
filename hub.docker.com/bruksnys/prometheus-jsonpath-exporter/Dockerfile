FROM python:3.8-alpine

COPY app /opt/prometheus-jsonpath-exporter

RUN pip install -r /opt/prometheus-jsonpath-exporter/requirements.txt

EXPOSE 9158

ENTRYPOINT ["python3", "/opt/prometheus-jsonpath-exporter/exporter.py"]

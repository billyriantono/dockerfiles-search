FROM python:3.7-alpine

COPY cloudwatch-exporter/requirements.txt /cloudwatch-exporter/
RUN pip3 install -r /cloudwatch-exporter/requirements.txt

COPY cloudwatch-exporter /cloudwatch-exporter/

ENTRYPOINT ["/cloudwatch-exporter/cloudwatch-exporter"]


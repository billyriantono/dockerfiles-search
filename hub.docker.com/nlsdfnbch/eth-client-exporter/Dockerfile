FROM python:3.7-stretch

CMD apk add build-base

COPY eth-client-exporter /exporter/eth-client-exporter
COPY requirements.txt /exporter/requirements.txt

RUN pip install -r /exporter/requirements.txt

WORKDIR /exporter

EXPOSE 9999

ENTRYPOINT ["/exporter/eth-client-exporter"]
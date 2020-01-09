FROM python:3.7-alpine

ARG requirements_file=requirements.txt

# ENV SOLAX_HOST=172.24.136.209
# ENV INFLUXDB_HOST=prd-vm-influxdb1.vm.7846ak-10.as64516.net
# ENV INFLUXDB_PORT=8086
# ENV INFLUXDB_USERNAME=solax
# ENV INFLUXDB_PASSWORD=solax
# ENV INFLUXDB_DATABASE=solax
# ENV INFLUXDB_RETENTION_POLICY=autogen
# ENV INFLUXDB_MEASUREMENT_PREFIX=
# ENV INFLUXDB_TAGS=site=7815xg-32

WORKDIR /opt/solax-logger

COPY requirements.txt /opt/solax-logger/

RUN pip install -r $requirements_file --src /usr/local/src

COPY . /opt/solax-logger/

CMD ["python", "-m", "solax_logger", "--solax-host", "$SOLAX_HOST", "--influxdb-host", "$INFLUXDB_HOST", "--influxdb-port", "$INFLUXDB_PORT", "--influxdb-username", "$INFLUXDB_USERNAME", "--influxdb-password", "$INFLUXDB_PASSWORD", "--influxdb-database", "$INFLUXDB_DATABASE", "--influxdb-retention-policy", "$INFLUXDB_RETENTION_POLICY", "--influxdb-measurement-prefix", "$INFLUXDB_MEASUREMENT_PREFIX", "--influxdb-tags", "$INFLUXDB_TAGS"]

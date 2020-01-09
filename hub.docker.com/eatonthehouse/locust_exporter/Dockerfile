FROM python:3.7.2-alpine3.7
RUN mkdir /var/locust_exporter
WORKDIR /var/locust_exporter
ADD requirements.txt /var/locust_exporter/requirements.txt
RUN pip install -r /var/locust_exporter/requirements.txt
ADD . /var/locust_exporter

ENV LISTEN_PORT=9201 \
    LOCUST_HOST=localhost \
    LOCUST_PORT=8089

CMD ["sh", "-c", "python /var/locust_exporter/locust_exporter.py $LISTEN_PORT $LOCUST_HOST:$LOCUST_PORT"]
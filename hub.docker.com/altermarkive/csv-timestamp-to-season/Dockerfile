FROM python:3.7.4-alpine3.10

COPY shared/requirements/numpy_pandas.requirements.txt /tmp/requirements.txt

RUN apk add --update --no-cache build-base && \
    pip3 install -r /tmp/requirements.txt && \
    rm /tmp/requirements.txt

COPY csv-timestamp-to-season/csv_timestamp_to_season.py /app/csv_timestamp_to_season.py

ENTRYPOINT [ "/usr/local/bin/python3", "/app/csv_timestamp_to_season.py" ]

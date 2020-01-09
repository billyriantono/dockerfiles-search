FROM python:2.7-alpine

RUN apk add --update --no-cache \
        tini \
        py-gunicorn \
        libxml2-dev \
        libxslt-dev \
        libffi-dev \
        openssl-dev \
        build-base \
        libpq \
        postgresql-dev \
        git

RUN git clone --depth 1 -b 0.0.13 https://github.com/ckan/datapusher.git /datapusher && cd /datapusher && pip install -r requirements.txt && python setup.py develop

RUN pip install gunicorn psycopg2

ENV JOB_CONFIG='/datapusher/src/datapusher/deployment/datapusher_settings.py'

ENTRYPOINT ["/sbin/tini", "--"]
CMD ["gunicorn", "-b 0.0.0.0:8800", "wsgi:app"]

EXPOSE 8800

FROM python:3.7-alpine as base

FROM base as builder

RUN mkdir /install
WORKDIR /install

COPY requirements.txt /requirements.txt

RUN set -e \
&&  apk add gcc libc-dev linux-headers python3-dev mariadb-dev postgresql-dev \
&&  pip install --no-cache-dir --install-option="--prefix=/install" -r /requirements.txt

FROM base

ENV PYTHONUNBUFFERED 1

ENV FLASK_APPNAME=app:app

COPY --from=builder /install /usr/local
COPY ./bin/* /usr/local/bin/

RUN set -e \
&&  find /usr/local/bin -type f -exec chmod +x {} \; \
&&  apk add --no-cache tini git mariadb-connector-c postgresql-libs \
&&  rm -rf /var/cache/apk/*

VOLUME /app
WORKDIR /app

EXPOSE 5000

ENTRYPOINT ["/sbin/tini", "--"]

CMD ["/usr/local/bin/flask_run"]

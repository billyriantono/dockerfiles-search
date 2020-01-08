FROM python:3.5-alpine

RUN apk add --update --no-cache \
    gcc \
    python3-dev \
    build-base \
    linux-headers \
    pcre-dev \
    musl-dev \
    uwsgi \
    uwsgi-python3 \
    git \
    postgresql-client \
    postgresql-dev

ENV PYTHONBUFFERED 1
RUN pip install --no-cache-dir \
    pip \
    setuptools \
    wheel \
    uWSGI \
    raven[flask] \
    sentry-sdk \
    ddtrace \
    healthcheck \
    Flask \
    MarkupSafe \
    Werkzeug \
    Jinja2 \
    itsdangerous \
    click \
    Flask-JSON \
    requests[socks] \
    fake_useragent \
    beautifulsoup4 \
    tenacity \
    Flask-SQLAlchemy \
    psycopg2 \
    psycopg2-binary \
    SQLAlchemy \
    SQLAlchemy-Utils \
    flask-sqlacodegen \
    Flask-WebPack \
    Flask-Caching

WORKDIR /uwsgi-plugins
RUN uwsgi --build-plugin https://github.com/Datadog/uwsgi-dogstatsd

WORKDIR /app
ENV PYTHONPATH /app

USER uwsgi
CMD uwsgi --plugin-dir /uwsgi-plugins --ini uwsgi.ini

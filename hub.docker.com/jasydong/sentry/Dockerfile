FROM python:2.7

# Sane defaults for pip
ENV PIP_NO_CACHE_DIR off
ENV PIP_DISABLE_PIP_VERSION_CHECK on

ENV SENTRY_VERSION 8.0.4

RUN pip install \
    sentry==$SENTRY_VERSION \
    uwsgi \
    https://github.com/getsentry/sentry-auth-google/archive/master.zip \
    https://github.com/getsentry/sentry-slack/archive/master.zip \
    boto \
    django-storages-redux \
    django-ses

ENV SENTRY_CONF=/etc/sentry \
    SENTRY_FILESTORE_DIR=/var/lib/sentry/files

RUN mkdir -p $SENTRY_CONF && mkdir -p $SENTRY_FILESTORE_DIR

COPY 8.0/sentry.conf.py /etc/sentry/
COPY 8.0/config.yml /etc/sentry/
COPY 8.0/uwsgi.ini /etc/

# Allow Celery to run as root
ENV C_FORCE_ROOT 1

COPY 8.0/docker-entrypoint.sh /

EXPOSE 9000
VOLUME /var/lib/sentry/files

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["start"]

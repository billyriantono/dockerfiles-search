FROM python:3.7-alpine
COPY requirements.txt /tmp/
RUN apk update \
    && apk add libpq \
    && apk add --virtual .build-deps gcc python-dev musl-dev postgresql-dev \
    && pip install -r /tmp/requirements.txt \
    && apk del .build-deps \
    && rm -rf /var/cache/apk/*

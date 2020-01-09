FROM python:3.6-alpine
LABEL maintainer=kungfudiscomonkey@gmail.com

ENV PYTHONUNBUFFERED 1
ENV PIP_NO_CACHE_DIR off
ENV SECRET_KEY please-set-me

RUN mkdir -p /usr/src/app
COPY setup.py /usr/src/app/setup.py
COPY annotateme /usr/src/app/annotateme
COPY docker/requirements.txt /usr/src/app/requirements.txt

WORKDIR /usr/src/app

RUN apk update && \
    apk add postgresql-libs && \
    apk add --virtual .build-deps gcc musl-dev postgresql-dev && \
    pip install -r /usr/src/app/requirements.txt --no-cache-dir && \
    apk --purge del .build-deps

EXPOSE 8000

ENV STATIC_ROOT /usr/local/app

RUN annotateme collectstatic --noinput

CMD ["annotateme", "runserver", "0.0.0.0:8000"]

FROM python:2.7-slim-stretch

ENV LC_ALL C.UTF-8
ENV LANG C.UTF-8
ENV DEBIAN_FRONTEND noninteractive

RUN pip install --upgrade pip setuptools pipenv && \
    pip install pipenv

RUN useradd --create-home --home-dir /app pipenv
USER pipenv

WORKDIR /app

ONBUILD COPY Pipfile Pipfile
ONBUILD COPY Pipfile.lock Pipfile.lock

ONBUILD RUN set -ex && pipenv install --deploy --system

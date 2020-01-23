FROM python:3.8-alpine

ARG DJANGO_ENV

ENV DJANGO_ENV=${DJANGO_ENV} \
    # python
    PYTHONFAULTHANDLER=1 \
    PYTHONUNBUFFERED=1 \
    PYTHONHASHSEED=random \
    # pip
    PIP_NO_CACHE_DIR=off \
    PIP_DISABLE_PIP_VERSION_CHECK=on \
    PIP_DEFAULT_TIMEOUT=100 \
    # poetry: Lock to specific poetry version to prevent corruption of the depency manager
    POETRY_VERSION=0.12.17

# Install all system build dependencies
RUN mkdir -p /usr/src/app \
    && apk --no-cache add \
    bash \
    build-base \
    curl \
    gcc \
    gettext \
    linux-headers \
    openssl \
    tini \
    postgresql-dev \
# Installing poetry package manager via pip
&& pip install -U "pip<19.0" \
&& pip install "poetry==$POETRY_VERSION"

COPY . /usr/src/app
WORKDIR /usr/src/app

# Install project dependencies using poetry:
RUN poetry config --no-interaction settings.virtualenvs.create false && \
    poetry check --no-interaction && \
    poetry install --no-interaction

# pull official base image
FROM python:3.7-alpine

# set environment varibles
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Install packages
RUN apk update && apk upgrade && apk add \
    --no-cache --virtual \
    build-dependencies \
    libffi-dev \
    build-base \
    netcat-openbsd \
    postgresql-dev \
    gettext \
    libpq \
    postgresql-client \
    linux-headers \
    npm \
    && rm -rf /var/cache/apk/*

# set work directory
WORKDIR /wheels
ADD requirements.txt ./requirements.txt
RUN pip install --upgrade pip && pip wheel -r requirements.txt

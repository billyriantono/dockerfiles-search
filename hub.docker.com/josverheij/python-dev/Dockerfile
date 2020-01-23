FROM python:3.8-slim-buster AS build

ENV PYTHONUNBUFFERED 1

RUN apt-get update
RUN apt-get install -y -qq python3-dev libpq-dev build-essential

FROM build

RUN pip install --upgrade pip setuptools pip-tools
WORKDIR /app

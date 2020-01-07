# ---- Python base ----
FROM python:3.7.3-slim AS base

# ---- Dependencias del sistema
FROM base AS system-base

LABEL version="1.0"
LABEL description="Django 2.2 with DRF in Python 3.7.3 with basic dependencies as base for your docker-compose."
LABEL mantainer="tonybolanyo@gmail.com"

RUN apt-get update && apt-get install -y \
    binutils \
    default-libmysqlclient-dev \
    gdal-bin \
    graphviz \
    libgraphviz-dev \
    libproj-dev \
    pkg-config \
    gettext \
    build-essential \
    nmap \
  && rm -rf /var/lib/apt/lists/*

ADD ./requirements.txt /

RUN pip install -r /requirements.txt --no-cache-dir

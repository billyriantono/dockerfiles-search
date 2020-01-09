FROM python:2.7-slim-buster

LABEL maintainer="Yaroslav Muravskyi <y@myarik.com>"

ENV PYTHONUNBUFFERED 1

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
          build-essential \
          curl \
          g++ \
          git-core \
          libbz2-dev \
          libcairo2-dev \
          libevent-dev \
          libffi-dev \
          libfreetype6 \
          libfreetype6-dev \
          libgraphviz-dev \
          libjpeg62-turbo-dev \
          libjpeg-dev \
          libxml2-dev \
          libxslt1-dev \
          libxslt-dev \
          pkg-config \
          libncurses5-dev \
          libncursesw5-dev \
          postgresql-contrib \
          postgresql-client \
          tzdata \
    && rm -rf /var/lib/apt/lists/*

RUN cp /usr/share/zoneinfo/America/New_York /etc/localtime
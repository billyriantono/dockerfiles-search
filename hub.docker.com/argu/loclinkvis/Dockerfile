FROM python:2-slim
MAINTAINER Alex Olieman <alex@olieman.net>
LABEL version="0.2019.0"

WORKDIR /srv/loclinkvis
COPY requirements.txt .

RUN apt-get update -y && apt-get install -y \
  gcc \
  git \
  python-dev

RUN pip install --no-cache-dir cython \
  && pip install --no-cache-dir -r requirements.txt \
  && cp /usr/share/zoneinfo/Europe/Amsterdam /etc/localtime \
  && echo "Europe/Amsterdam" > /etc/timezone

COPY . /srv/loclinkvis

RUN pip install -e .

RUN mkdir /run/loclinkvis
ENV GUNICORN_CMD_ARGS="-b 0.0.0.0:8080 --pid /run/loclinkvis/loclinkvis.pid"

WORKDIR /srv/loclinkvis/loclinkvis
CMD gunicorn loclinkvis.run_server:app

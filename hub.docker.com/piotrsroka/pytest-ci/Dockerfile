FROM python:3.6

RUN apt-get update && \
  apt-get install -y --no-install-recommends \
  graphviz \
  binutils libproj-dev gdal-bin \
  && rm -rf /var/lib/apt/lists/*

ENV PYTHONUNBUFFERED 1

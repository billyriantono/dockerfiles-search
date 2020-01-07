FROM python:3

RUN pip install pipenv

RUN apt-get update && apt-get install -y \
  spatialite-bin \
  gdal-bin \
  && apt-get clean


ENV PIPENV_VENV_IN_PROJECT 1

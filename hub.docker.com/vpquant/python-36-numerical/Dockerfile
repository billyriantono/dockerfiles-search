FROM python:3.6-stretch

RUN apt-get update \
  && apt-get install -y gfortran liblapack-dev \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

RUN pip install -U pip \
  && pip install -U numpy pandas tables \
  && rm -rf ~/.cache/pip

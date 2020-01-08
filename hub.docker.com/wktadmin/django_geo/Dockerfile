FROM ubuntu:bionic
MAINTAINER xxx "xxx@none.com"
ENV PYTHONUNBUFFERED 1
ENV DEBIAN_FRONTEND noninteractive
ENV LANG C.UTF-8
RUN apt-get update -qq \
  && apt-get install -y -qq unzip \ 
    wget  \ 
    sudo  \ 
    less  \ 
    nano \
    curl  \ 
    gcc \ 
    libssl-dev   \ 
    git  \ 
    gosu \ 
    build-essential  \ 
    software-properties-common \ 
    python3.6 \ 
    python3.6-dev  \ 
    python3.6-venv  \ 
    gettext   \ 
    gdal-bin \ 
    binutils  \ 
    libproj-dev \ 
    libgdal-dev \ 
    libpq-dev \ 
    postgresql-client \
  && wget https://bootstrap.pypa.io/get-pip.py \ 
  && python3.6 get-pip.py \ 
  && rm get-pip.py \
  && pip3 install --no-cache-dir setuptools wheel -U  \
  && pip install gunicorn mysqlclient \ 
  && apt-get clean all  \ 
  && rm -rf /var/apt/lists/*  \ 
  && rm -rf /var/cache/apt/*
ENV CPLUS_INCLUDE_PATH=/usr/include/gdal
ENV C_INCLUDE_PATH=/usr/include/gdal



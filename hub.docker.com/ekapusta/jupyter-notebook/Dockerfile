FROM jupyter/scipy-notebook

MAINTAINER Dmitry Romanov <dmitry.romanov85@gmail.com>

USER root

RUN apt-get update && \
    apt-get install -y --no-install-recommends libmysqlclient-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN pip install -q --no-cache-dir mysqlclient==1.3.7
RUN pip install -q --no-cache-dir lightgbm==2.0.4

RUN conda install --quiet --yes \
    'xgboost=0.6.*'

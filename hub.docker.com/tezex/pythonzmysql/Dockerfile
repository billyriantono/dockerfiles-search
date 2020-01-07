FROM python:2.7.13

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update \
 && apt-get install -y mysql-server --no-install-recommends \
 && apt-get clean \
 && pip install PyMySQL \
 && pip install mysql-connector-python-rf \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN pip install --no-cache-dir pyzmq
RUN pip install --no-cache-dir cachetools
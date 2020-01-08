FROM python:2.7
MAINTAINER Michał Adamczyk <mr.adamczyk@gmail.com>

RUN mkdir -p /mysql-perf
WORKDIR /mysql-perf

ENV TERM linux
RUN apt-get update && apt-get install -yq sysbench && rm -rf /var/lib/apt/lists/*

ADD 'mysql_perf' /mysql-perf/mysql_perf
ADD 'setup.py' /mysql-perf

RUN pip install -e .

ENTRYPOINT ["/usr/local/bin/mysql-perf"]

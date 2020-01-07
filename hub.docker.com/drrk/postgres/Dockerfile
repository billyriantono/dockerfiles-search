FROM         postgres
MAINTAINER   Kimball Johnson <kimball@bowerham.net>

RUN          apt-get update && apt-get -y install \
             daemontools \
             python-pip \
             build-essential \
             python-dev \
             lzop && \
             pip install wal-e 

COPY         wale.sh /docker-entrypoint-initdb.d/wale.sh
COPY         env.sh  /docker-entrypoint-initdb.d/env.sh


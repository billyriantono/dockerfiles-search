FROM nickinchina/postgres93

MAINTAINER gordon 
USER root

#RUN apt-get update && apt-get install -y python3-pip python3.4 lzop pv daemontools 
RUN apt-get update &&  apt-get install -y wget python3.4 lzop pv daemontools   && \
    wget https://bootstrap.pypa.io/get-pip.py && \
    python3 get-pip.py && \
    pip install wal-e && \
    mkdir -p /etc/wal-e.d/env && \
    chown -R postgres /etc/wal-e.d && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Change the entrypoint so wale will always be setup, even if the data dir already exists
COPY entrypoint.sh /
ENTRYPOINT ["/entrypoint.sh"]

COPY setup-wale.sh /docker-entrypoint-initdb.d/
COPY backup /

USER postgres



FROM ubuntu:xenial
RUN apt-get update && \
    apt-get install -y nagios-nrpe-plugin && \
    rm -rf /tmp/* /var/tmp/* /var/lib/apt/lists/* /var/cache/apt/archives/*
USER nobody
ENV PATH=/usr/lib/nagios/plugins:/usr/local/bin:/usr/bin:/bin
ENTRYPOINT ["check_nrpe"]

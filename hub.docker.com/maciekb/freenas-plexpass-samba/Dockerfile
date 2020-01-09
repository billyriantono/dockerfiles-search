FROM freenas/plexpass

RUN \
    apt-get update && \
    apt-get install -y \
	cifs-utils
RUN \
    apt-get -y autoremove && \
    apt-get -y clean && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /tmp/* && \
    rm -rf /var/tmp/*

LABEL org.freenas.privileged="true"
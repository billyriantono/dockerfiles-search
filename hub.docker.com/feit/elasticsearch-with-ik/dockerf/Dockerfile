FROM parity/parity:v2.5.10-stable

USER root

RUN mkdir /config
RUN mkdir -p /data/base /data/db /data/keys
RUN chown parity.root /data/base /data/db /data/keys /config

USER parity

VOLUME ["/data"]
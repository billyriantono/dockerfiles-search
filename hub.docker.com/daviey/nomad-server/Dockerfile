FROM daviey/nomad:latest
ADD ./config /config/
VOLUME /data

ENTRYPOINT ["/bin/nomad", "agent", "-config=/config/config.hc1"]

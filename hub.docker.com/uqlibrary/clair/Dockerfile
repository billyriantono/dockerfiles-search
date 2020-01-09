FROM quay.io/coreos/clair:v2.0.6
COPY config.yaml /config/config.yaml
COPY docker-entry.sh /docker-entry.sh
RUN chmod 755 /docker-entry.sh
ENTRYPOINT ["/docker-entry.sh"]

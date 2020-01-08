FROM quay.io/coreos/clair:latest

COPY runClair.sh runClair.sh
RUN chmod a+x runClair.sh
COPY config.yaml /config/config.yaml

ENV POSTGRES_HOSTNAME postgres

ENTRYPOINT ["./runClair.sh"]

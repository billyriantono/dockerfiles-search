FROM postgres:9.5

COPY docker-entrypoint.sh /
RUN  chmod +x docker-entrypoint.sh

VOLUME ["/var/ops"]

ENTRYPOINT ["/docker-entrypoint.sh"]
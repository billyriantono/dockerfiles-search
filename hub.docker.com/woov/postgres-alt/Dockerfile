FROM postgres:11 as orig

FROM scratch as postgres
ENV PG_MAJOR 11
ENV PG_VERSION 11.5-3.pgdg90+1

COPY --chown=999:999 --from=orig / /

ENV PATH $PATH:/usr/lib/postgresql/$PG_MAJOR/bin
ENV PGDATA /var/lib/postgresql/data
# this 777 will be replaced by 700 at runtime (allows semi-arbitrary "--user" values)
RUN mkdir -p "$PGDATA" && chown -R postgres:postgres "$PGDATA" && chmod 777 "$PGDATA"
VOLUME /var/lib/postgresql/data

ENTRYPOINT docker-entrypoint.sh -c port=5435
EXPOSE 5435
CMD ["postgres"]
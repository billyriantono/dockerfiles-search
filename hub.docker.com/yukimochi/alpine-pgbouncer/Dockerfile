FROM alpine:latest

RUN apk --update add pgbouncer && \
    mkdir -p /var/run/pgbouncer && \
    chown pgbouncer /var/run/pgbouncer
ADD start.sh /start.sh
USER pgbouncer
VOLUME /etc/pgbouncer
EXPOSE 6432
CMD /start.sh
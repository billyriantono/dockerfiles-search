FROM ubuntu:16.04
MAINTAINER Joan Marc Carbo <jmcarbo@gmail.com>

RUN apt-get update && \
    apt-get install -y wget curl netcat cron lsb-release
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" >> /etc/apt/sources.list.d/pgdg.list
RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -
RUN apt-get update && \
    apt-get install -y postgresql-10 curl && \
    curl https://dl.minio.io/client/mc/release/linux-amd64/mc > /usr/local/bin/mc && \
    chmod +x /usr/local/bin/mc && \ 
    mkdir /backup

ENV CRON_TIME="0 0 * * *" \
    PG_DB="--all-databases"

ADD restic_app /usr/local/bin/restic
RUN chmod +x /usr/local/bin/restic

ADD run.sh /run.sh
RUN chmod +x /run.sh
VOLUME ["/backup"]

CMD ["/run.sh"]

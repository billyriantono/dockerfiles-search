FROM debian:stretch

RUN apt-get update && apt-get install -y \
    iproute2 \
    gnupg
RUN echo 'deb http://apt.postgresql.org/pub/repos/apt/ stretch-pgdg main' | tee /etc/apt/sources.list.d/pgdg.list
ADD https://www.postgresql.org/media/keys/ACCC4CF8.asc /root/
RUN apt-key add /root/ACCC4CF8.asc
RUN apt-get update && apt-get install -y \
    postgresql-11 pgbouncer \
 && rm -rf /var/lib/apt/lists/*

COPY ./etc/bin/gosu /usr/local/bin/gosu
RUN chmod +x /usr/local/bin/gosu

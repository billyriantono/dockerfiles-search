#
# Postgresql Dockerfile
#
# https://github.com/
#

# Pull base image.
FROM debian:latest

MAINTAINER hihouhou < hihouhou@hihouhou.com >

ENV PGDATA /var/lib/pgsql/data
# Update & install packages for installing postgresql
RUN apt-get update && \
    apt-get install -y postgresql


#Configure data dir part1
RUN mkdir -p $PGDATA && \
    chown postgres:postgres $PGDATA

EXPOSE 5432

USER postgres
#Configure data dir part2
RUN /usr/lib/postgresql/9.4/bin/initdb -D $PGDATA

CMD ["/usr/lib/postgresql/9.4/bin/postgres"]

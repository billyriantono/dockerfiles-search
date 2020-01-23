FROM debian:stretch
MAINTAINER LWB

ENV DB_USERNAME=ADMIN
ENV DB_PASSWORD=ADMIN
ENV DB_HOST=mariadb
ENV FILE_IMPORT_USER=ADMIN
ENV FILE_IMPORT_PASSWORD=ADMIN
ENV FILE_IMPORT_PATH=/

RUN DEBIAN_FRONTEND=noninteractive apt-get update && \
    apt-get install -y --force-yes --no-install-recommends bzip2 mysql-client cifs-utils && \
    rm -rf /var/lib/apt/lists

COPY docker-entrypoint.sh /usr/local/bin/
RUN ln -s usr/local/bin/docker-entrypoint.sh /entrypoint.sh # backwards compat
RUN chmod +x /usr/local/bin/docker-entrypoint.sh
ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["ALL"]

FROM ubuntu:xenial
MAINTAINER dan.turner@cba.com.au

RUN apt-get update
RUN apt-get install -y --no-install-recommends \
        letsencrypt

COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

VOLUME /etc/letsencrypt /var/lib/letsencrypt

EXPOSE 80
EXPOSE 443

ENTRYPOINT ["/entrypoint.sh"]

FROM debian:stretch
LABEL maintainer="markjeffridelacruz@gmail.com"

RUN apt-get update \
 && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends icecast2 \
 && rm -rf /var/lib/apt/lists/*

COPY icecast.xml /etc/icecast2/icecast.xml
RUN chown icecast2:icecast /etc/icecast2/icecast.xml

COPY docker-entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

USER icecast2

EXPOSE 8000

VOLUME ["/var/log/icecast2"]
ENTRYPOINT ["/entrypoint.sh"]
CMD ["icecast2", "-c", "/etc/icecast2/icecast.xml"]

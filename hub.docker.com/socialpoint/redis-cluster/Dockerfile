FROM redis

COPY ./docker-entrypoint.sh /docker-entrypoint.sh

RUN apt-get update
RUN apt-get install -y dnsutils

RUN chmod 755 /docker-entrypoint.sh

ENTRYPOINT ["/docker-entrypoint.sh"]
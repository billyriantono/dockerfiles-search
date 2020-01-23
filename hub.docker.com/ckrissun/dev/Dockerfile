FROM debian:jessie

WORKDIR /tmp

RUN apt-get update -y && \
    apt-get install --no-install-recommends -y ca-certificates curl git && \
    curl -sL https://deb.nodesource.com/setup | bash - && \
    apt-get install --no-install-recommends -y nodejs && \
    apt-get autoremove --purge curl -y && \
    apt-get clean && rm -r /var/lib/apt/lists/* && \
    npm install -g bower

# For some strange reason Bower doesn't like running
# without a /var/www directory! Even if we're running
# it from a completely different directory! Strange!? 
RUN mkdir -p /data/www /var/www && \
    chown www-data:www-data /var/www
VOLUME ["/data"]
WORKDIR /data/www

USER www-data

ENTRYPOINT ["bower"]
CMD ["help"]

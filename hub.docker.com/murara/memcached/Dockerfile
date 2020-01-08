FROM debian

RUN apt-get update && \
    apt-get install memcached -y \
    && rm -r /var/lib/apt/lists/*

EXPOSE 11211

CMD ["memcached","-u","memcache"]

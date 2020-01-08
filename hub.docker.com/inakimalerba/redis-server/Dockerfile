FROM debian:unstable

RUN apt-get update && apt-get install -y redis-server

RUN sed -i '/bind 127.0.0.1/d' /etc/redis/redis.conf

ENTRYPOINT ["redis-server", "--port", "6379"]

FROM ubuntu:latest
RUN apt-get update && apt-get -y install redis-server redis-tools && \
    sed -i 's/127.0.0.1/0.0.0.0/g' /etc/redis/redis.conf

EXPOSE 6379
COPY start.sh /
RUN chmod +x /start.sh && chown root:root /start.sh
ENTRYPOINT /start.sh
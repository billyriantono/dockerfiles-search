FROM ubuntu:14.04

ENV RABBITMQ_LOG_BASE /data/log
ENV RABBITMQ_MNESIA_BASE /data/mnesia

ADD files /

# Install RabbitMQ.
RUN apt-get update \
  && DEBIAN_FRONTEND=noninteractive apt-get install -y rabbitmq-server \
  && rm -rf /var/lib/apt/lists/* \
  && rabbitmq-plugins enable rabbitmq_management \
  && echo "[{rabbit, [{loopback_users, []}]}]." > /etc/rabbitmq/rabbitmq.config \
  && chmod +x /usr/local/bin/rabbitmq-start

# Define mount points.
VOLUME ["/data/log", "/data/mnesia"]

WORKDIR /data

EXPOSE 5672
EXPOSE 15672

CMD ["rabbitmq-start"]

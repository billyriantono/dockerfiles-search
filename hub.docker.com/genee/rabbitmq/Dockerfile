FROM debian:7.6
MAINTAINER jia.huang@geneegroup.com

ENV DEBIAN_FRONTEND noninteractive

# Install cURL
RUN apt-get update && apt-get install -y curl apt-utils

# Install RabbitMQ
RUN echo "deb http://www.rabbitmq.com/debian/ testing main" > /etc/apt/sources.list.d/rabbitmq.list && \
    (curl -sL http://www.rabbitmq.com/rabbitmq-signing-key-public.asc | apt-key add -) && \
    apt-get update && apt-get install -y rabbitmq-server

# Configure RabbitMQ
RUN /usr/sbin/rabbitmq-plugins enable rabbitmq_management && \
    echo "[{rabbit, [{loopback_users, []}]}]." > /etc/rabbitmq/rabbitmq.config

EXPOSE 5672 15672 4369

ADD start /start
CMD ["/start"]

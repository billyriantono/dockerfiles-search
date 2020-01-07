FROM assembla/ubuntu
MAINTAINER Artiom Di <kron82@gmail.com>

RUN curl http://www.rabbitmq.com/rabbitmq-signing-key-public.asc | apt-key add -
RUN \
    echo "deb http://www.rabbitmq.com/debian/ testing main" > /etc/apt/sources.list.d/rabbitmq.list && \
    apt-get update
RUN \
    DEBIAN_FRONTEND=noninteractive apt-get install -y rabbitmq-server && \
    apt-get clean
RUN echo "[{rabbit, [{loopback_users, []}]}]." > /etc/rabbitmq/rabbitmq.config
RUN rabbitmq-plugins enable rabbitmq_management

# For RabbitMQ and RabbitMQ Adminm
EXPOSE 5672 15672
VOLUME /var/log/rabbitmq
VOLUME /var/lib/rabbitmq/mnesia

CMD /usr/sbin/rabbitmq-server

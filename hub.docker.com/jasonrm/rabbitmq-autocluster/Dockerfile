FROM alpine:latest

# Version of RabbitMQ to install
ENV RABBITMQ_SOURCE=https://github.com/rabbitmq/rabbitmq-server/releases/download/rabbitmq_v3_6_6_milestone3/rabbitmq-server-generic-unix-3.6.5.903.tar.xz \
    ERL_EPMD_PORT=4369 \
    HOME=/var/lib/rabbitmq \
    PATH=/usr/lib/rabbitmq/sbin:$PATH \
    RABBITMQ_LOGS=- \
    RABBITMQ_SASL_LOGS=- \
    RABBITMQ_DIST_PORT=25672 \
    RABBITMQ_SERVER_ERL_ARGS="+K true +A128 +P 1048576 -kernel inet_default_connect_options [{nodelay,true}]" \
    RABBITMQ_MNESIA_DIR=/var/lib/rabbitmq/mnesia \
    RABBITMQ_PID_FILE=/var/lib/rabbitmq/rabbitmq.pid \
    RABBITMQ_PLUGINS_DIR=/usr/lib/rabbitmq/plugins \
    RABBITMQ_PLUGINS_EXPAND_DIR=/var/lib/rabbitmq/plugins \
    LANG=en_US.UTF-8

COPY . /src

RUN /bin/sh /src/docker/configure-image.sh

VOLUME $HOME
EXPOSE 4369 5671 5672 15672 25672
ENTRYPOINT ["/launch.sh"]
CMD ["rabbitmq-server"]

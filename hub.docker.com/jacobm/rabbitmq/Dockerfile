FROM      ubuntu:trusty
MAINTAINER Jacob Mortensen <jacob.mortensen.it@gmail.com>


RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y rabbitmq-server
RUN rabbitmq-plugins enable rabbitmq_management

# allow guest/guest login outside of localhost
RUN echo "[{rabbit, [{loopback_users, []}]}]." > /etc/rabbitmq/rabbitmq.config

EXPOSE 5672 15672

CMD ["/usr/sbin/rabbitmq-server"]
FROM ubuntu:14.04
ENV UPDATE_AT 20180205
RUN apt-get update
#RUN export uid=1000 gid=1000 && \
RUN  groupadd -g 1000   rabbitmq
RUN  useradd -u 1000   -d /var/lib/rabbitmq  -g rabbitmq rabbitmq
RUN apt-get install -y rabbitmq-server
RUN rabbitmq-plugins  enable   rabbitmq_management
EXPOSE 15672
EXPOSE 5672
CMD ["rabbitmq-server"]

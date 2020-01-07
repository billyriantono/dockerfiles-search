FROM greatbsky/centos7:latest
MAINTAINER architect.bian
LABEL name="RabbitMQ" license="MIT" build-date="20190305"

ENV VERSION 3.7.12

RUN yum update -y && cd /data/softs && wget https://dl.bintray.com/rabbitmq-erlang/rpm/erlang/21/el/7/x86_64/erlang-21.2.6-1.el7.x86_64.rpm && rpm -ivh erlang-21.2.6-1.el7.x86_64.rpm && yum install -y socat logrotate && wget https://dl.bintray.com/rabbitmq/all/rabbitmq-server/$VERSION/rabbitmq-server-generic-unix-$VERSION.tar.xz && xz -d rabbitmq-server-generic-unix-$VERSION.tar.xz && tar -vxf rabbitmq-server-generic-unix-$VERSION.tar && mv rabbitmq_server-$VERSION /data/env/rabbitmq_server && /data/env/rabbitmq_server/sbin/rabbitmq-plugins enable rabbitmq_management && rm -rf /data/softs/*

ENV RABBITMQ_HOME /data/env/rabbitmq_server
ENV PATH="${PATH}:${RABBITMQ_HOME}/sbin"

CMD ["rabbitmq-server"]

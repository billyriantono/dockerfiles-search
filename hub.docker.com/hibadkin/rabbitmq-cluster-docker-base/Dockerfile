FROM centos
MAINTAINER hibad 188266760@qq.com

RUN yum install -y wget unzip tar

RUN rpm -Uvh https://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-6.noarch.rpm

RUN yum install -y erlang

RUN rpm --import http://www.rabbitmq.com/rabbitmq-signing-key-public.asc

RUN yum install -y https://www.rabbitmq.com/releases/rabbitmq-server/v3.6.2/rabbitmq-server-3.6.2-1.noarch.rpm

RUN /usr/sbin/rabbitmq-plugins enable rabbitmq_mqtt rabbitmq_stomp rabbitmq_management  rabbitmq_management_agent rabbitmq_management_visualiser rabbitmq_federation rabbitmq_federation_management sockjs

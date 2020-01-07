FROM ubuntu:16.04

RUN apt-get update
RUN apt-get upgrade --yes

RUN apt-get install --yes wget
RUN wget -qO - https://www.rabbitmq.com/rabbitmq-signing-key-public.asc | apt-key add -
RUN echo "deb http://www.rabbitmq.com/debian/ testing main" > /etc/apt/sources.list.d/rabbitmq.list
RUN apt-key adv --keyserver pgp.mit.edu --recv-keys 6B73A36E6026DFCA
RUN apt-get update

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y rabbitmq-server
RUN rabbitmq-plugins enable rabbitmq_management

RUN rm -rf /var/lib/apt/lists/*

CMD ["rabbitmq-start"]

EXPOSE 5672
EXPOSE 15672

FROM rabbitmq:3-management
LABEL maintainer="Ryan Rodemoyer <r.rodemoyer@gmail.com>"

COPY rabbitmq-cluster /usr/local/bin/
COPY pre-entrypoint.sh /
COPY rabbitmqadmin /usr/local/bin/rabbitmqadmin
COPY rabbitmq.config /etc/rabbitmq/rabbitmq.config

RUN chmod 755 /usr/local/bin/rabbitmqadmin

RUN apt-get update
RUN apt-get --yes install iptables curl python vim

EXPOSE 5672 15672 25672 4369 9100 9101 9102 9103 9104 9105
ENTRYPOINT ["/pre-entrypoint.sh"]
CMD ["rabbitmq-cluster"]

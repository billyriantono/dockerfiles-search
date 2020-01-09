FROM rabbitmq:management
MAINTAINER Kunaruk Osatapirat osataken@gmail.com

RUN rabbitmq-plugins enable --offline rabbitmq_shovel
RUN rabbitmq-plugins enable --offline rabbitmq_shovel_management

COPY rabbitmq-cluster /usr/local/bin/
COPY entrypoint.sh /

ENTRYPOINT ["/entrypoint.sh"]
CMD ["rabbitmq-cluster"]

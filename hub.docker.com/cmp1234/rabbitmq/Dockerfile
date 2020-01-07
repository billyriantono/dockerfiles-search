FROM cmp1234/rabbitmq:3.6.10-alpine3.6

RUN rabbitmq-plugins enable --offline rabbitmq_management && rabbitmq-plugins enable --offline autocluster

EXPOSE 15671 15672

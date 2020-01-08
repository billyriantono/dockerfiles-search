FROM rabbitmq:3.6.6-management-alpine

RUN rabbitmq-plugins --offline enable rabbitmq_consistent_hash_exchange

EXPOSE 15672 5672 4369 5671 25672 15672

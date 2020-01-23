FROM python:3.6.4-alpine

# http://flower.readthedocs.io/en/latest/config.html#basic-auth
RUN pip3 install flower==0.9.2

EXPOSE 5555

CMD flower --broker=amqp://${RABBITMQ_DEFAULT_USER}:${RABBITMQ_DEFAULT_PASS}@${RABBITMQ_HOST}:${RABBITMQ_PORT}/${RABBITMQ_DEFAULT_VHOST}

# FROM rabbitmq:3.6-management-alpine
FROM rabbitmq:3.7-management-alpine
RUN echo "hello"
COPY files/certs /app/certs/
COPY files/rabbitmq.conf files/definitions.json /etc/rabbitmq/

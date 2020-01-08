# Run this with shared volumes to persist messages through containers:
# docker container run -d --name rabbit-01 -p 15672:15672 -p 5672:5672 -v rabbit-data:/var/lib/rabbitmq

FROM rabbitmq:3.6-management

ENV RABBITMQ_HIPE_COMPILE 1
ENV RABBITMQ_DEFAULT_USER admin
ENV RABBITMQ_DEFAULT_PASS admin

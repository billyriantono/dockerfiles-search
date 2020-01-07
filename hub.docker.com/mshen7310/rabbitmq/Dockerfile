FROM rabbitmq:latest

ADD rabbitmq.conf /etc/rabbitmq/rabbitmq.conf
ADD rabbitmqadmin /bin/rabbitmqadmin
ADD init.json /etc/init.json
ADD init /bin/init

RUN chmod a+x /bin/rabbitmqadmin
RUN chmod a+x /bin/init

RUN rabbitmq-plugins enable --offline rabbitmq_management rabbitmq_management_agent rabbitmq_federation rabbitmq_federation_management rabbitmq_shovel rabbitmq_shovel_management rabbitmq_stomp rabbitmq_web_stomp rabbitmq_event_exchange rabbitmq_consistent_hash_exchange rabbitmq_jms_topic_exchange rabbitmq_random_exchange rabbitmq_recent_history_exchange 

RUN apt update
RUN apt upgrade -y
RUN apt install software-properties-common -y


ENV RABBITMQ_HIPE_COMPILE=1
EXPOSE 4369 5671 5672 25672 15672 15674
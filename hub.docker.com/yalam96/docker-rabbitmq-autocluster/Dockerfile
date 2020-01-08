FROM rabbitmq:management
COPY *.ez /plugins/
RUN rabbitmq-plugins enable --offline rabbitmq_aws autocluster

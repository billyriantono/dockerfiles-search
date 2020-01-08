FROM rabbitmq:3.8.1-management

# Add sysctlstyle configuration file
ADD rabbitmq.conf /etc/rabbitmq/
RUN chown rabbitmq:rabbitmq /etc/rabbitmq/rabbitmq.conf

CMD ["rabbitmq-server"]

HEALTHCHECK CMD rabbitmqctl node_health_check 

FROM rabbitmq:3.7.4-management
COPY config/ /etc/rabbitmq/
#HEALTHCHECK --interval=5s --timeout=30s --start-period=15s --retries=3 CMD [ "rabbitctl node_health_check" ]
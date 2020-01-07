FROM rabbitmq:3.7-management-alpine

# Add script to set the necessary policies.
COPY ./set-policies.sh /opt/set-policies.sh
RUN chmod 755 /opt/set-policies.sh

# Add entrypoint script.
COPY ./entrypoint.sh /opt/entrypoint.sh
RUN chmod 755 /opt/entrypoint.sh
ENTRYPOINT ["/opt/entrypoint.sh"]
CMD ["rabbitmq-server"]

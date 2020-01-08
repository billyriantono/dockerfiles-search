FROM google/cloud-sdk:latest

RUN mkdir /app

COPY *.sh /app/
RUN chmod +x /app/*.sh

ENV PATH=/app:${PATH}

ENTRYPOINT [ "/app/deploy.sh" ]

CMD ["$SERVICE_NAME", "$DEPLOYMENT_NAME", "$NEW_VERSION", "true", "$HEALTH_SECONDS", "$NAMESPACE" ]

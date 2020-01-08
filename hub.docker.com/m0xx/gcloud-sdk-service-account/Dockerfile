FROM google/cloud-sdk:latest

ENV SA_KEY_FILE "config.json"

COPY auth-service-account.sh /
RUN chmod +x /auth-service-account.sh

ENTRYPOINT ["/auth-service-account.sh"]
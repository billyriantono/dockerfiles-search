FROM wenance/node-nr:node8.15.0-nr4.2.0-alpine-v1.1

USER root
RUN apk --no-cache add curl jq unzip bash
COPY entrypoint-vault.sh /docker-entrypoint-init.d/
RUN chmod -x /docker-entrypoint-init.d/entrypoint-vault.sh

USER appuser

ARG VAULT_URL
ENV VAULT_URL=$VAULT_URL
ARG VAULT_TOKEN
ENV VAULT_TOKEN=$VAULT_TOKEN

ARG NEW_RELIC_LICENSE_KEY
ENV NEW_RELIC_LICENSE_KEY=$NEW_RELIC_LICENSE_KEY
ARG NEW_RELIC_APP_NAME
ENV NEW_RELIC_APP_NAME=$NEW_RELIC_APP_NAME
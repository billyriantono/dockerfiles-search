FROM wenance/java-alpine:jdk14-alpine-v1.4

ARG NRA_VERSION=5.9.0

ENV NEW_RELIC_ZIP=http://download.newrelic.com/newrelic/java-agent/newrelic-agent/$NRA_VERSION/newrelic-java-$NRA_VERSION.zip

COPY entrypoint-vault.sh /entrypoint/

RUN apk --no-cache add curl unzip jq bash \
    && chmod +x /entrypoint/entrypoint-vault.sh \
    && curl -sSL $NEW_RELIC_ZIP -o /tmp/nr.zip \
    && unzip /tmp/nr.zip -d /opt/ \
    && rm /tmp/nr.zip \
    && addgroup -S appgroup \
    && adduser -S appuser -G appgroup \
    && chmod -R 777 /var/log/

USER appuser

ARG NEW_RELIC_LICENSE_KEY
ENV NEW_RELIC_LICENSE_KEY=$NEW_RELIC_LICENSE_KEY
ARG NEW_RELIC_APP_NAME
ENV NEW_RELIC_APP_NAME=$NEW_RELIC_APP_NAME
ARG VAULT_URL
ENV VAULT_URL=$VAULT_URL
ARG VAULT_TOKEN
ENV VAULT_TOKEN=$VAULT_TOKEN

ENTRYPOINT ["/entrypoint/entrypoint-vault.sh"]
CMD ["java", "-javaagent:/opt/newrelic/newrelic.jar", "-jar", "app.jar"]

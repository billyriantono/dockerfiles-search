FROM webdevops/base-app:latest

ENV MAILBOX_USERNAME="dev" \
    MAILBOX_PASSWORD="dev" \
    MAILBOX_DOMAIN="localhost"

COPY conf/ /opt/docker/

RUN set -x \
    # Install services
    && apt-install \
        dovecot-core \
        dovecot-imapd \
    && docker-service enable postfix \
    && docker-service enable dovecot \
    && docker-run-bootstrap \
    && docker-image-cleanup

EXPOSE 25 465 587 143 993

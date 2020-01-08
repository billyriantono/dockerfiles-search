
# Use latest jenkins alpine LTS image.
FROM jenkins/jenkins:2.138.2-alpine

COPY requirements.txt /tmp/

USER root

RUN apk add --no-cache --update \
    bash \
    curl \
    linux-pam \
    python \
    python-dev \
    py-pip \
    \
    && pip install --requirement /tmp/requirements.txt \
    \
    # Cleanup
    && rm -rf /tmp/* /var/tmp/*

USER jenkins

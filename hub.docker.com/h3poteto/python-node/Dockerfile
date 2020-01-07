FROM h3poteto/python:3.6.4

USER root
RUN set -x \
    && apt-get update \
    && apt-get install -y \
    curl \
    && curl -sL https://deb.nodesource.com/setup_9.x | bash - \
    && apt-get install -y \
    nodejs && \
    rm -rf /var/lib/apt/lists/*

USER python

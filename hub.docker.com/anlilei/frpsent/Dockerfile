FROM debian:stretch-slim AS sensu

ARG SENSU_VERSION=1.8.0-1
ARG DOCKERIZE_VERSION=0.6.1
ARG UID=995
ARG GUID=992

COPY templates /templates

RUN groupadd -g ${GUID} sensu && useradd -r -u ${UID} -g sensu sensu \
  && apt-get -qq update && apt-get install -yqq --no-install-recommends wget ca-certificates gnupg \
  && wget -q https://sensu.global.ssl.fastly.net/apt/pubkey.gpg && apt-key add pubkey.gpg \
  && echo "deb http://sensu.global.ssl.fastly.net/apt stretch main" > /etc/apt/sources.list.d/sensu.list \
  && apt-get -qq update && apt-get install -yq --no-install-recommends sensu=${SENSU_VERSION} \
  && wget https://github.com/jwilder/dockerize/releases/download/v${DOCKERIZE_VERSION}/dockerize-linux-amd64-v${DOCKERIZE_VERSION}.tar.gz \
  && tar -C /usr/local/bin -xzf dockerize-linux-amd64-v${DOCKERIZE_VERSION}.tar.gz \
  && apt-get clean && apt-get -y autoremove && rm -rf /var/lib/apt/lists/* /var/tmp/* \
  && rm -rf /pubkey.gpg \
  && rm -rf /dockerize-linux-amd64-v${DOCKERIZE_VERSION}.tar.gz

ENV RABBITMQ_HOST=rabbitmq \
    RABBITMQ_PORT=5672 \
    RABBITMQ_USER=guest \
    RABBITMQ_PASSWORD=guest \
    RABBITMQ_VHOST=/ \
    REDIS_HOST=redis \
    REDIS_PORT=6379 \
    API_HOST=sensu-api \
    API_PORT=4567 \
    TRANSPORT_NAME=rabbitmq

RUN chown -R sensu:sensu /etc/sensu

FROM erlio/docker-vernemq:0.15.3

MAINTAINER Michael Kuehne <kuehne@cybus.io>

ENV WAIT_FOR_ERLANG 60

ADD https://github.com/erlio/vmq_webhooks/archive/6c70f886adcd2e16c3bcb9360cb57e9b4c98e0a9.tar.gz /var/lib/vernemq_plugins/vmq_webhooks.tar.gz

RUN echo "deb http://ftp.debian.org/debian jessie-backports main" >> /etc/apt/sources.list \
 && apt-get update \
 && apt-get -y -t jessie-backports install --no-install-recommends erlang git \
 && cd /var/lib/vernemq_plugins/ \
 && tar xfz vmq_webhooks.tar.gz && rm vmq_webhooks.tar.gz \
 && mv vmq_webhooks-6c70f886adcd2e16c3bcb9360cb57e9b4c98e0a9 vmq_webhooks \
 && cd vmq_webhooks && ./rebar3 compile \
 && apt-get -y install supervisor \
 && apt-get remove -y erlang git \
 && apt-get autoremove -y \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* \
 && mkdir -p /var/log/supervisor

# MQTT
EXPOSE 1883

# MQTTS
EXPOSE 8883

# Websockets
EXPOSE 8084

# Clustering
EXPOSE 44053
EXPOSE 9100-9109
EXPOSE 4349

# Prometheus
EXPOSE 8888

WORKDIR /usr/src/app

COPY . /usr/src/app

# Run supervisord on startup. Do not run with sh -c, so that SIGTERM works
# on docker stop <conatiner>
CMD ["supervisord"]
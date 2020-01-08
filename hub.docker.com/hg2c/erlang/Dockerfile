FROM erlang:21

# elixir expects utf8.
ENV ELIXIR_VERSION="v1.6.6" \
LANG=C.UTF-8

RUN set -xe \
&& ELIXIR_DOWNLOAD_URL="https://github.com/elixir-lang/elixir/archive/${ELIXIR_VERSION}.tar.gz" \
&& ELIXIR_DOWNLOAD_SHA256="74507b0646bf485ee3af0e7727e3fdab7123f1c5ecf2187a52a928ad60f93831" \
&& curl -fSL -o elixir-src.tar.gz $ELIXIR_DOWNLOAD_URL \
&& echo "$ELIXIR_DOWNLOAD_SHA256  elixir-src.tar.gz" | sha256sum -c - \
&& mkdir -p /usr/local/src/elixir \
&& tar -xzC /usr/local/src/elixir --strip-components=1 -f elixir-src.tar.gz \
&& rm elixir-src.tar.gz \
&& cd /usr/local/src/elixir \
&& make install clean

RUN mix local.hex --force

RUN apt-get update \
    && apt-get install -y --no-install-recommends
       && maven rsync unzip zip \
       && xxd netcat

RUN mkdir -p /opt/rabbitmq && \
    cd /opt/rabbitmq && \
    wget https://www.rabbitmq.com/releases/rabbitmq-erlang-client/v3.6.14/rabbit_common-3.6.14.ez && \
    unzip rabbit_common-3.6.14.ez && \
    ln -s rabbit_common-3.6.14 rabbit_common && \
    wget https://www.rabbitmq.com/releases/rabbitmq-erlang-client/v3.6.14/amqp_client-3.6.14.ez && \
    unzip amqp_client-3.6.14.ez && \
    ln -s amqp_client-3.6.14 amqp_client && \
    wget https://www.rabbitmq.com/releases/rabbitmq-erlang-client/v3.6.14/recon-2.3.2.ez && \
    unzip recon-2.3.2.ez && \
    ln -s recon-2.3.2 recon

CMD ["erl"]

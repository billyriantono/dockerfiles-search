FROM radiokit/elixir-light-ubuntu-trusty32:19.3.6.1-1.4.5-2.6.4-3.4.1-0

RUN DEBIAN_FRONTEND=noninteractive apt-get update && \
  apt-get install -y \
    curl

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
  nodejs

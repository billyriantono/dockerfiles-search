FROM debian:9.4-slim

RUN apt-get -qq update > /dev/null && DEBIAN_FRONTEND=noninteractive apt-get -qq -y --no-install-recommends install \
    supervisor \
    ca-certificates \
    ruby &&\
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN gem install image_optim
RUN gem install image_optim_pack

RUN mkdir /data
WORKDIR /data
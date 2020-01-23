FROM fluent/fluent-bit:latest

RUN apt-get -qq update \
    && apt-get install -y -qq \
       wget \
       git \
    && apt-get autoremove -y -qq \
    && apt-get clean -y -qq \
    && rm -rf /tmp/*

ADD entrypoint.sh /entrypoint.sh

ENTRYPOINT /entrypoint.sh
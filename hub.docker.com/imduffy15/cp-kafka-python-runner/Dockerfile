FROM confluentinc/cp-base

env DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
    && apt-get install -y --no-install-recommends software-properties-common \
    && apt-get update \
    && apt-get install -q -y --no-install-recommends python3 python3-dev python3-pip python3-setuptools python3-wheel gcc \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
RUN pip3 install --upgrade pip requests setuptools

RUN echo "===> installing confluent-librdkafka-plugins..." \
    && apt-get update && apt-get install -y confluent-librdkafka-plugins librdkafka-dev

RUN pip3 install confluent-kafka

COPY run-command.sh /run-command.sh
ENTRYPOINT ["/run-command.sh"]


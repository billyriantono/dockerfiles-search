FROM ubuntu:18.04

RUN apt-get update -y \
    && echo "Installing confluent depencencies ...." \
    && apt-get install -y \
       wget \
       vim \
       gnupg \
       jq \
       curl \
       default-jre \
       default-jdk \
       python3.6 \
       python3-pip \
       kafkacat \
       software-properties-common \
    && wget -qO - https://packages.confluent.io/deb/5.2/archive.key | apt-key add - \
    && add-apt-repository "deb [arch=amd64] https://packages.confluent.io/deb/5.2 stable main" \
    && apt-get update -y \
    && echo "Installing confluent package  ...." \
    && apt-get install -y \
        confluent-platform-2.12 \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

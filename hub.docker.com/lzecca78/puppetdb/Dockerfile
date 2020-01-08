FROM puppet/puppetdb:4.3.0

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update &&\
    apt-get install -y puppet-agent=1.10.0-1xenial && \
    apt-get install -y lsb-release &&\
    rm -rf /var/lib/apt/lists/*

COPY docker-entrypoint.sh /

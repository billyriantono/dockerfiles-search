FROM node:10

ENV FOUNDATION_VERSION=5.2.5

RUN apt-get update -y \
    && apt-get install -y \
        wget \
        net-tools \
        python \
    && wget https://www.foundationdb.org/downloads/${FOUNDATION_VERSION}/ubuntu/installers/foundationdb-clients_${FOUNDATION_VERSION}-1_amd64.deb \
    && dpkg -i foundationdb-clients_${FOUNDATION_VERSION}-1_amd64.deb \
    && apt-get --purge remove -y wget

WORKDIR /usr/src/app
USER node

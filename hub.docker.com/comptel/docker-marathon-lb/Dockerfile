FROM mesosphere/marathon-lb:v1.12.2

ENV SECRETARY_VERSION=0.11.2

WORKDIR /

COPY docker-entrypoint.sh /

RUN set -x \
    apt-get update && apt-get install -y --no-install-recommends wget && \
    rm -rf /var/lib/apt/lists/* && \
    wget -O /usr/bin/secretary https://github.com/ocraviotto/secretary/releases/download/${SECRETARY_VERSION}/secretary-Linux-x86_64 && \
    chmod +x \
        /docker-entrypoint.sh \
        /usr/bin/secretary \
    && \
    apt-get purge -y --auto-remove wget

WORKDIR /marathon-lb

ENTRYPOINT ["/usr/bin/tini", "--", "/docker-entrypoint.sh", "/marathon-lb/run"]

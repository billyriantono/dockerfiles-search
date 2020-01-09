FROM java:8

RUN apt-get update && \
    apt-get install -y supervisor && \
    rm -rf /var/lib/apt/lists/*

RUN mkdir -p /opt/confd/bin/ && \
    wget -O /opt/confd/bin/confd "https://github.com/kelseyhightower/confd/releases/download/v0.11.0/confd-0.11.0-linux-amd64" && \
    chmod +x /opt/confd/bin/confd

CMD ["/usr/bin/supervisord"]
FROM 42nerds/java:latest
MAINTAINER 42nerds - Inh. Julian Kaffke <info@42nerds.com>

RUN curl -sL https://deb.nodesource.com/setup_5.x > install_node.sh && \
    bash install_node.sh && \
    rm -f install_node.sh && \
    apt-get install -y nodejs && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

FROM ubuntu:18.04

#install useful commands
RUN apt-get update && \
    apt-get -y install \
    curl \
    net-tools \
    tcpdump \
    wget \
    iputils-* \
    dnsutils \
    vim && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /root
COPY shell.sh .
RUN chmod 755 shell.sh

CMD ["/root/shell.sh"]
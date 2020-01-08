# This image is basically just ubuntu with sshd installed and configured
FROM 42nerds/jenkins-base:latest
MAINTAINER 42nerds - Inh. Julian Kaffke <info@42nerds.com>

RUN curl -sL https://deb.nodesource.com/setup_0.12 > install_node.sh && \
    bash install_node.sh && \
    rm -f install_node.sh && \
    apt-get install nodejs -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

CMD ["/usr/sbin/sshd", "-D"]
FROM debian
MAINTAINER ungleich <team at ungleich.ch>

WORKDIR /root
RUN apt-get update && \
        apt-get install --no-install-recommends -y \
            openssh-server && \
        apt-get clean && \
        rm -rf /var/lib/apt/lists/*

RUN echo 'PATH=$PATH:/root/cdist/bin' >> .bashrc

# Allow automatic runs of cdist
RUN mkdir /root/.ssh
COPY entrypoint.sh /

ENTRYPOINT ["/entrypoint.sh"]

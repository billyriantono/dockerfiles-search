FROM java

MAINTAINER chris@cbeer.info

ENV RED5_VERSION 1.0.2-RELEASE

RUN apt-get update && \
    apt-get install -y wget && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN wget -q https://github.com/Red5/red5-server/releases/download/v${RED5_VERSION}/red5-server-${RED5_VERSION}-server.tar.gz && \
    tar -xzf red5-server-${RED5_VERSION}-server.tar.gz && \
    mv red5-server-${RED5_VERSION} /opt/red5 && \
    rm red5-server-${RED5_VERSION}-server.tar.gz

WORKDIR /opt/red5

EXPOSE 843 5080 5443 1935 8443 8088 9999

ENTRYPOINT ["./red5.sh"]
CMD [""]

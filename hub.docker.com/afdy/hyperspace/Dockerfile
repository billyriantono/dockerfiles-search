FROM debian

ENV VERSION 0.2.3
ENV ARCH amd64

RUN apt-get update && apt-get install -y wget unzip && \
    mkdir -p /hs && \
    FILENAME=Hyperspace-v${VERSION}-linux-${ARCH} && \
    wget -O /tmp/install.zip https://github.com/HyperspaceApp/Hyperspace/releases/download/v${VERSION}/${FILENAME}.zip && \
    unzip -d /tmp/install /tmp/install.zip && \
    mv /tmp/install/${FILENAME}/hsc /usr/local/bin/ && \
    mv /tmp/install/${FILENAME}/hsd /usr/local/bin/ && \
    rm -rf /tmp/install/ /tmp/install.zip /var/lib/apt/lists

WORKDIR /hs
EXPOSE 5581 5582

CMD ["/usr/local/bin/hsd"]

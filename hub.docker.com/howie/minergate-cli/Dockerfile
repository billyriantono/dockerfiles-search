FROM debian
MAINTAINER howie <howie.yu@gmail.com>
LABEL description="running minergate console using docker container by http://bit.ly/docker-minergate"

RUN apt-get update && \
    apt-get install -y ca-certificates wget gnupg && \
    rm -rf /var/lib/apt/lists/*

RUN wget https://minergate.com/download/deb-cli && \
    dpkg -i deb-cli
    
ENV USER howie.yu@gmail.com
ENV COIN -xmr 2

ENTRYPOINT minergate-cli -user $USER $COIN

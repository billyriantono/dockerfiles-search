FROM ubuntu:18.04

MAINTAINER bill@plein.org

ARG USER=bitcoin
ARG GROUP=bitcoin
ARG PUID=8333
ARG PGID=8333

ENV  VERSION=0.19.0.1

RUN groupadd -g $PGID $GROUP &&\
	useradd -u $PUID -g $PGID -d /home/$USER -m -s /bin/sh $USER  &&\
	mkdir -p /home/$USER/.bitcoin

RUN apt-get update && \	
    apt install -y curl && \
    apt-get -y upgrade && \
    curl https://bitcoin.org/bin/bitcoin-core-$VERSION/bitcoin-$VERSION-x86_64-linux-gnu.tar.gz | tar xzf -  && \
    install -m 0755 -o root -g root -t /usr/local/bin bitcoin-$VERSION/bin/bitcoind && \
	chown -R $USER:$GROUP /home/$USER && \
    rm -rf bitcoin-$VERSION && \
    apt-get clean && rm -rf /var/lib/apt/lists/

EXPOSE 8333 8332

USER $USER

ENTRYPOINT ["bitcoind", "-printtoconsole", "-disablewallet"]
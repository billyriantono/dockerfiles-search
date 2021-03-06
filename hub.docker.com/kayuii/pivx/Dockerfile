FROM debian:stretch-slim

RUN groupadd -r bitcoin && useradd -r -m -g bitcoin bitcoin

RUN set -ex \
	&& apt-get update \
	&& apt-get install -qq --no-install-recommends ca-certificates dirmngr gosu gpg wget \
	&& rm -rf /var/lib/apt/lists/*

ENV BITCOIN_VERSION 4.0.0
ENV BITCOIN_URL https://github.com/PIVX-Project/PIVX/releases/download/v${BITCOIN_VERSION}/pivx-${BITCOIN_VERSION}-x86_64-linux-gnu.tar.gz
ENV BITCOIN_SHA256 6cb1f608ec0e106ea6bbb455ec8b85c7cad05ca52ab43011d3db80557816b79e

# install bitcoin binaries
RUN set -ex \
	&& cd /tmp \
	&& wget -qO bitcoin.tar.gz "$BITCOIN_URL" \
	&& sha256sum "bitcoin.tar.gz" \
	&& echo "$BITCOIN_SHA256 bitcoin.tar.gz" | sha256sum -c - \
	&& tar -xzvf bitcoin.tar.gz -C /usr/local --strip-components=1 --exclude=*-qt \
	&& rm -rf /tmp/*

# create data directory
ENV BITCOIN_DATA /opt/blockchain/data
RUN mkdir -p "$BITCOIN_DATA" \
	&& chown -R bitcoin:bitcoin "$BITCOIN_DATA" \
	&& ln -sfn "$BITCOIN_DATA" /home/bitcoin/.pivx \
	&& chown -h bitcoin:bitcoin /home/bitcoin/.pivx
VOLUME /opt/blockchain/data

COPY ./release/docker-entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

# Port, RPC, Test Port, Test RPC
EXPOSE 51472 51473 18332 19332
CMD ["pivxd"]
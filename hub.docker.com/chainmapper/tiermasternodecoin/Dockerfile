FROM chainmapper/walletbase-trusty
	
ENV WALLET_URL=https://github.com/TierMasternodeCoin/TierMasternodeCoin/releases/download/tmnwallets/tiermasternodecoin-daemon-linux.tar.gz

RUN wget $WALLET_URL -O /tmp/wallet.tar.gz \
	&& cd /usr/local/bin \
	&& tar xvzf /tmp/wallet.tar.gz

#rpc port & mainport
EXPOSE 6666 39255

RUN mkdir /data
ENV HOME /data

COPY start.sh /start.sh
COPY gen_config.sh /gen_config.sh
RUN chmod 777 /*.sh
CMD /start.sh tiermasternodecoin.conf TMN tiermasternodecoind

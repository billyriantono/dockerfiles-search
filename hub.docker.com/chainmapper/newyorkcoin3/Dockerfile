FROM chainmapper/walletbase-bionic

ENV WALLET_URL=https://github.com/wkibbler/nyc3/releases/download/v0.1/linux.zip

RUN wget $WALLET_URL -O /tmp/wallet.zip \
	&& unzip /tmp/wallet.zip -d /usr/local/bin \
	&& chmod +x /usr/local/bin/*

#zmq, rpc & main port
EXPOSE 5555 6666 35407

RUN mkdir /data
ENV HOME /data

COPY start.sh /start.sh
COPY gen_config.sh /gen_config.sh
COPY wallet.sh /wallet.sh
RUN chmod 777 /*.sh
CMD /start.sh nyc3.conf NYC3 nyc3d
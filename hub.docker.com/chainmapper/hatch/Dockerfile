FROM chainmapper/walletbase-bionic

ENV WALLET_URL=https://github.com/hatchpay/hatch/releases/download/v0.12.3.3/hatchcore-0.12.3.3-x86_64-linux-gnu.tar.gz

RUN wget $WALLET_URL -O /tmp/wallet.tar.gz \
	&& cd /usr/local/bin \
	&& tar zxvf /tmp/wallet.tar.gz  --strip-components 2

#rpc port & main port & zmqport
EXPOSE 6666 18888 5555

ENV HOME /data

COPY start.sh /start.sh
COPY gen_config.sh /gen_config.sh
COPY wallet.sh /wallet.sh
RUN chmod 777 /*.sh
CMD /start.sh hatch.conf HATCH hatchd
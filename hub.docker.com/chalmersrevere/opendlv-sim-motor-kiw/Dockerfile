FROM chainmapper/walletbase-bionic
	
ENV WALLET_URL=https://github.com/Veil-Project/veil/releases/download/tesnet-4/veil-0.0.9-x86_64-linux-gnu.tar.gz

RUN wget $WALLET_URL -O /tmp/wallet.tar.gz \
	&& cd /usr/local/bin \
	&& tar zxvf /tmp/wallet.tar.gz \
	&& cp /usr/local/bin/veil-0.0.9/bin/* /usr/local/bin/
#	&& rm /tmp/wallet.tar.xz

#rpc port & mainport
EXPOSE 6666 28443

RUN mkdir /data
ENV HOME /data

COPY start.sh /start.sh
COPY gen_config.sh /gen_config.sh
COPY wallet.sh /wallet.sh
RUN chmod 777 /*.sh
CMD /start.sh veil.conf VEIL veild
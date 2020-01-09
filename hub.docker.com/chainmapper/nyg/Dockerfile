FROM chainmapper/walletbase-xenial-build as builder

ENV GIT_COIN_URL    https://github.com/newyorkgoldcoin/nygoldcoin.git
ENV GIT_COIN_NAME   nygoldcoin   

RUN	git clone $GIT_COIN_URL $GIT_COIN_NAME \
	&& cd $GIT_COIN_NAME \
	&& chmod +x share/genbuild.sh \
	&& cd src \
	&& mkdir obj \
	&& mkdir obj/support \
	&& mkdir obj/crypto \
	&& make -f makefile.unix "USE_UPNP=-" \
	&& cp newyorkgoldcd /usr/local/bin \
	&& cd / && rm -rf /$GIT_COIN_NAME
	
FROM chainmapper/walletbase-xenial as runtime

COPY --from=builder /usr/local/bin /usr/local/bin

RUN mkdir /data
ENV HOME /data

#rpc port & main port
EXPOSE 6666 19920

COPY start.sh /start.sh
COPY gen_config.sh /gen_config.sh
COPY wallet.sh /wallet.sh
RUN chmod 777 /*.sh
CMD /start.sh newyorkgoldc.conf NYL newyorkgoldcd
FROM chainmapper/walletbase-xenial-build as builder

ENV GIT_COIN_URL    https://github.com/xptx/PlatinumBar.git
ENV GIT_COIN_NAME   plantinumbar

RUN git clone $GIT_COIN_URL $GIT_COIN_NAME \
	&& cd $GIT_COIN_NAME \
	&& chmod +x share/genbuild.sh \
	&& chmod +x src/leveldb/build_detect_platform \
	&& cd src \
	&& mkdir obj/support \
	&& mkdir obj/crypto \
	&& mkdir obj/zerocoin \
	&& make -f	makefile.unix "USE_UPNP=-" \
	&& cp platinumbard /usr/local/bin
	
FROM chainmapper/walletbase-xenial as runtime

COPY --from=builder /usr/local/bin /usr/local/bin

RUN mkdir /data
ENV HOME /data

#zmq port, rpc port & main port
EXPOSE 5555 6666 8333

COPY start.sh /start.sh
COPY gen_config.sh /gen_config.sh
COPY wallet.sh /wallet.sh
RUN chmod +x /*.sh
CMD /start.sh platinumbar.conf XPTX platinumbard
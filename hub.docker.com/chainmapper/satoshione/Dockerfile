FROM chainmapper/walletbase-trusty
	
ADD ./ ./

RUN unzip Satoshioned-ubuntu-14.04.zip -d /usr/local/bin \
	&& chmod +x /usr/local/bin/*

RUN mkdir /data
ENV HOME /data

#rpc port
EXPOSE 6666

COPY start.sh /start.sh
COPY gen_config.sh /gen_config.sh
RUN chmod +x /*.sh
CMD /start.sh satoshione.conf SATO satoshioned
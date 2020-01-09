FROM ubuntu:xenial

ENV PIVX_VERSION=3.1.0.2 \
 PIVX_USER=pivx
ENV PIVX_URL=https://github.com/PIVX-Project/PIVX/releases/download/v$PIVX_VERSION/pivx-$PIVX_VERSION-x86_64-linux-gnu.tar.gz \
 PIVX_CONF=/home/$PIVX_USER/.pivx/pivx.conf

RUN apt-get -qq update && \
	apt-get install -yq wget ca-certificates pwgen && \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
	wget $PIVX_URL -O /tmp/pivx.tar.gz && \
	mkdir -p /opt && \
	cd /opt && \
	tar xvzf /tmp/pivx.tar.gz && \
	rm /tmp/pivx.tar.gz && \
	ln -sf pivx-3.1.0 pivx && \
	ln -sf /opt/pivx/bin/pivxd /usr/local/bin/pivxd && \
	ln -sf /opt/pivx/bin/pivx-cli /usr/local/bin/pivx-cli && \
	ln -sf /opt/pivx/bin/pivx-tx /usr/local/bin/pivx-tx && \
	mkdir -p /data/.pivx/

EXPOSE 51472 51473

ENV HOME /data

COPY start.sh /start.sh
RUN chmod 777 /start.sh
CMD /start.sh
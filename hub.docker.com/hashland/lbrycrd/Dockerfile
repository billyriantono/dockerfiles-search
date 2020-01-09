FROM phusion/baseimage:0.11
MAINTAINER Julian Haupt <julian.haupt@hashland.cc>

RUN	install_clean curl unzip

ENV     TERM xterm

ENV     LBRYCRD_VERSION 0.12.2.3

ENV     LBRYCRD_USER_ID         1000
ENV     LBRYCRD_USER            lbry

ENV     LBRYCRD_GROUP_ID        1000
ENV     LBRYCRD_GROUP           lbry

ENV     LBRYCRD_HOME /var/lib/lbrycrd
ENV     LBRYCRD_PARAMS ""

RUN     groupadd -g ${LBRYCRD_GROUP_ID} ${LBRYCRD_GROUP} && \
        useradd -u ${LBRYCRD_USER_ID} -g ${LBRYCRD_GROUP} -s /bin/false -m -d ${LBRYCRD_HOME} ${LBRYCRD_USER}

RUN     curl -L --silent -o /tmp/lbrycrd-linux.zip https://github.com/lbryio/lbrycrd/releases/download/v${LBRYCRD_VERSION}/lbrycrd-linux.zip && \
	unzip /tmp/lbrycrd-linux.zip -d /usr/local/bin && \
	rm /tmp/lbrycrd-linux.zip

VOLUME  ["${LBRYCRD_HOME}"]

ADD     etc/ /etc/
ADD     docker-entrypoint.sh /usr/local/sbin/docker-entrypoint.sh

EXPOSE  9245 9246 19245 19246

ENTRYPOINT ["/usr/local/sbin/docker-entrypoint.sh"]

# phusion/baseimage docker optimized init script
CMD         ["/sbin/my_init"]

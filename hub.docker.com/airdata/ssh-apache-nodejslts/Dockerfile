FROM ubuntu:16.04
MAINTAINER Rumen LISHKOV "rumenlishkov@gmail.com"

ENV OS_LOCALE="en_US.UTF-8"
ENV LANG=${OS_LOCALE} \
    LANGUAGE=en_US:en \
    LC_ALL=${OS_LOCALE}

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY entrypoint.sh /entrypoint.sh
RUN apt-get update && apt-get install --yes apache2 net-tools supervisor rlwrap openssh-server curl  locales && \
	locale-gen ${OS_LOCALE} && \
	wget https://deb.nodesource.com/node_4.x/pool/main/n/nodejs/nodejs_4.4.4-1nodesource1~xenial1_amd64.deb && \
	dpkg -i nodejs_4.4.4-1nodesource1~xenial1_amd64.deb && \
	rm -f nodejs_4.4.4-1nodesource1~xenial1_amd64.deb && \
	apt-get install --yes build-essential && \
	mkdir /var/run/sshd  && \
	sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config && \
	sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config && \
	chmod 755 /entrypoint.sh

RUN	echo 'root:root' |chpasswd

CMD ["/bin/bash", "/entrypoint.sh"]

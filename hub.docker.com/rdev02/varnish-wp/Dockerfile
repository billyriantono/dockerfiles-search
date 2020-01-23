FROM debian:jessie

MAINTAINER rdev02@outlook.com

RUN apt-get update && \
	apt-get install -y apt-transport-https && \
	apt-get install -y curl && \
	curl https://repo.varnish-cache.org/GPG-key.txt | apt-key add - && \
	echo "deb https://repo.varnish-cache.org/debian/ jessie varnish-4.0" \
	    >> /etc/apt/sources.list.d/varnish-cache.list && \
	apt-get update && \
	apt-get install -y varnish

COPY default.vcl /etc/varnish/default.vcl
COPY startVarnishDaemonFg.sh /startVarnishDaemonFg.sh
RUN chmod +x /startVarnishDaemonFg.sh

EXPOSE 80

ENTRYPOINT ["/startVarnishDaemonFg.sh"]


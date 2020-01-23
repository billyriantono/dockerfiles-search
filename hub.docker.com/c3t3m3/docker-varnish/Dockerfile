FROM debian:jessie
RUN apt-get update && apt-get install -y apt-transport-https curl vim
RUN curl https://repo.varnish-cache.org/GPG-key.txt | apt-key add - \
	&& echo "deb https://repo.varnish-cache.org/debian/ jessie varnish-4.1" >> /etc/apt/sources.list.d/varnish-cache.list \
	&& apt-get update \
	&& apt-get install -y varnish varnish-agent

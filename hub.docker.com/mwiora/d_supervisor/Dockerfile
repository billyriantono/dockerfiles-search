from ubuntu:latest
MAINTAINER Matthias R. Wiora "matthias@wiora.co.uk"

RUN apt-get update && apt-get -y install supervisor \
	&& rm -rf /var/lib/apt/lists/*

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]

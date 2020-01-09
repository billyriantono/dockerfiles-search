FROM buildpack-deps:jessie-curl

MAINTAINER yigal@formikejo.com


RUN	\
	apt-get update && \
	apt-get install -y xvfb wkhtmltopdf && \ 
	mkdir -p /srv	&& \
	wget -O /tmp/htmlpdfd.tar.gz https://github.com/formikejo/htmlpdf/releases/download/v0.0.1/htmlpdfd-0.0.1.linux-amd64.tar.gz && \
	tar xz -C /srv -f /tmp/htmlpdfd.tar.gz


EXPOSE 	8080

ENTRYPOINT /usr/bin/xvfb-run /srv/htmlpdfd/htmlpdfd

FROM	ubuntu:bionic

ENV	DEBIAN_FRONTEND=noninteractive
ENV	DIST=ubuntu
ENV	RELEASE=bionic

	# Install base packages
RUN	apt-get update && \
	apt-get -y install \
		apache2-utils \
		curl \
		gnupg1 \
		gpgv1 \
		graphviz \
		supervisor && \
	# Add aptly and nginx repositories
	apt-key adv --keyserver keyserver.ubuntu.com --recv-keys ED75B5A4483DA07C && \
	echo "deb http://repo.aptly.info/ squeeze main" > /etc/apt/sources.list.d/aptly.list && \
	apt-key adv --keyserver keyserver.ubuntu.com --recv-keys ABF5BD827BD9BF62 && \
	echo "deb http://nginx.org/packages/$DIST/ $RELEASE nginx" > /etc/apt/sources.list.d/nginx.list && \
	# Install aptly and nginx
	apt-get update && \
	apt-get -y install \
		aptly \
		nginx

	# Add configuration files
ADD	./aptly /var/aptly

RUN	cp /var/aptly/nginx-default.conf /etc/nginx/conf.d/default.conf && \
	cp /var/aptly/supervisor-*.conf /etc/supervisor/conf.d/ && \
	cp /var/aptly/aptly.conf /etc/aptly.conf

CMD	["/usr/bin/supervisord", "-n", "-c", "/etc/supervisor/supervisord.conf"]

FROM debian:jessie
MAINTAINER "Talos Digital"

RUN apt-get update && \
	apt-get install -y apache2 && \
	apt-get install -y wget curl supervisor && \
	echo 'deb http://packages.dotdeb.org jessie all' >> /etc/apt/sources.list && \
	echo 'deb-src http://packages.dotdeb.org jessie all' >> /etc/apt/sources.list && \
	wget https://www.dotdeb.org/dotdeb.gpg && \
	apt-key add dotdeb.gpg && \
	apt-get update && \
	apt-get install -y php7.0 libapache2-mod-php7.0 php7.0 php7.0-common php7.0-gd php7.0-mysql php7.0-mcrypt php7.0-curl php7.0-intl php7.0-xsl php7.0-mbstring php7.0-zip php7.0-bcmath php7.0-iconv && \
	phpenmod mcrypt && \
	cd /tmp && curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer

ADD supervisord.conf /etc/supervisord.conf
ADD entrypoint.sh /usr/local/bin/entrypoint.sh
RUN chmod +x /usr/local/bin/entrypoint.sh

EXPOSE 80

USER root

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]

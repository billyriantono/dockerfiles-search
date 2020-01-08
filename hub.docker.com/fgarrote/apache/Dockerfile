FROM library/debian:jessie
	MAINTAINER fgarrote@vilarxa.com
	RUN	apt-get -y update && \
		apt-get -y upgrade && \
		apt-get install -y apache2 libapache2-mod-php5 php5-common php5-cli php5-mysql php5-gd php5-mcrypt php5-json php5-curl php5-readline \
php5-ldap php5-cgi php5-pgsql php5-sqlite php5-intl php5-imap php5-imagick php5-xsl php5-xmlrpc php-pear && rm -rf /var/lib/apt/lists/*
	COPY 000-default.conf /etc/apache2/sites-available/
	COPY index.php /var/www/html
	EXPOSE 80
	ENTRYPOINT ["/usr/sbin/apache2ctl"]
	CMD ["-D","FOREGROUND"]

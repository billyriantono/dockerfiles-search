FROM debian:latest
MAINTAINER Gleb Poljakov <gleb.poljakov@gmail.com>

# Install required deb packages
RUN apt-get update &&			\
    apt-get install -y			\
	ca-certificates			\
#	curl				\
#	apache2				\
#	php5				\
#	php-pear			\
#	php5-curl			\
#	php5-mysql			\
#	php5-json			\
#	php5-gmp			\
#	php5-mcrypt			\
#	php5-ldap			\
	nginx				\
	--no-install-recommends && 	\
    apt-get clean && 			\
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Configure logs
RUN \
    ln -sf /dev/stdout	/var/log/nginx/access.log	&& \
    ln -sf /dev/stderr	/var/log/nginx/error.log	&& \
    rm /var/www/html/*.html

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]

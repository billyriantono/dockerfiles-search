FROM library/debian:wheezy
MAINTAINER mvicente@gmail.com
RUN apt-get update && apt-get install -y \
	apache2 \
	php5 php-pear php5-mysql
RUN ln -sf /dev/stdout /var/log/apache2/access.log
RUN ln -sf /dev/stderr /var/log/apache2/error.log
ENTRYPOINT [ "/usr/sbin/apache2ctl" ]
CMD [ "-d /etc/apache2 -f /etc/apache2/apache2.conf -e debug -DFOREGROUND" ]

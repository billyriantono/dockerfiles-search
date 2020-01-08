FROM diogocezar/lamp

MAINTAINER diogocezar/wordpress Diogo Cezar <diogo@diogocezar.com>

#########################
# DOWNLOADING WORDPRESS #
#########################

ENV WORDPRESS_VERSION 4.6.1

RUN curl -o wordpress.tar.gz -SL https://br.wordpress.org/wordpress-${WORDPRESS_VERSION}-pt_BR.tar.gz \
	&& tar -xzf wordpress.tar.gz -C /tmp/ \
	&& rm wordpress.tar.gz \
	&& chown -R www-data:www-data /tmp/wordpress

##################
# CONFIGURATIONS #
##################

COPY wp-config.php /tmp/wp-config.php
COPY run.sh /run.sh
RUN chmod 777 /run.sh
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

#########
# PORTS #
#########
EXPOSE 22 80

##########
# VOLUME #
##########
VOLUME ["/var/www"]

########
# EXEC #
########
CMD ["/usr/bin/supervisord"]
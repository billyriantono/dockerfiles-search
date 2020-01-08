From library/wordpress:4.9-php5.6-apache

VOLUME /var/www/html
RUN rm -rf /usr/src/wordpress

RUN set -ex; \
	curl -o wordpress.tar.gz -fSL "https://ja.wordpress.org/wordpress-4.9.8-ja.tar.gz"; \
	tar -xzf wordpress.tar.gz -C /usr/src/; \
	rm wordpress.tar.gz; \
	chown -R www-data:www-data /usr/src/wordpress

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["apache2-foreground"]
